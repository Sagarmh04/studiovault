# Resource Module: Inventory & Availability

## 1. Asset Classes
* **Fixed Assets:** Cameras, Lenses, Lights, Drones. (Tracked by Serial Number).
* **Spaces:** Physical Rooms (e.g., "Green Screen Floor").
* **Human:** Photographers, Editors, Makeup Artists.

## 2. The "Lock" Mechanism
* **Goal:** Prevent double-booking.
* **Logic:** * Every Booking consumes specific resources for a specific time slot.
    * *Conflict Check:* `IF (Asset_A is Reserved) AND (New_Booking requires Asset_A) -> REJECT`.

## 3. Maintenance & Status
* **States:** Available, Booked, Maintenance, Lost/Stolen.
* **Logs:** Custody chain tracking. "Who had the Sony A7iii last?"

# Database Schema (Cloudflare D1 / SQLite)

## 1. Design Philosophy
* **SQL Dialect:** SQLite.
* **Identity:** Text-based IDs (CUID or Prefixed UUIDs like `usr_123`, `org_xyz`) for easy sharding.
* **Concurrency:** Optimistic Locking via `version` column on all mutable tables.
* **Flexibility:** Use `_json` columns for config/settings to avoid schema migration fatigue.

## 2. Core Tables (Identity)

### `organizations`
* `id` (PK, TEXT): Tenant ID.
* `name` (TEXT).
* `config_json` (TEXT): Settings, Currency, Logo URL.
* `version` (INT): For locking.

### `branches`
* `id` (PK, TEXT).
* `org_id` (FK, TEXT).
* `name` (TEXT).
* `address_json` (TEXT).

### `users`
* `id` (PK, TEXT): Matches Firebase UID.
* `org_id` (FK, TEXT).
* `email` (TEXT, UNIQUE Index).
* `role` (TEXT): 'owner', 'manager', 'staff'.

## 3. CRM & Operations

### `clients`
* `id` (PK, TEXT).
* `branch_id` (FK, TEXT): Clients are scoped to branch.
* `phone` (TEXT, Index): Critical for POS lookup.
* `profile_json` (TEXT): Address, GST, Family details.
* `total_spend` (REAL): Cached value for speed.

### `projects`
* `id` (PK, TEXT).
* `branch_id` (FK, TEXT).
* `client_id` (FK, TEXT).
* `status` (TEXT): 'inquiry', 'shooting', 'editing', 'completed'.
* `start_date` (INT): Unix Timestamp.
* `details_json` (TEXT): Dynamic fields based on Project Type (Wedding vs Commercial).
* **Indexes:** `(branch_id, status)`, `(branch_id, start_date)`.

### `quick_orders` (Walk-in/POS)
* `id` (PK, TEXT).
* `branch_id` (FK, TEXT).
* `total_amount` (REAL).
* `items_json` (TEXT): Array of items sold `[{id, qty, price}]`.
* `created_at` (INT).

## 4. Finance (Phase 1 Draft)
* `invoices` table linked to `projects` or `quick_orders`.
* `transactions` table for payments.