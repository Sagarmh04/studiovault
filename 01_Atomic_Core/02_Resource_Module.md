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

```
-- 4. Finance & Money (The Missing Piece)

-- A. Invoices (The Request for Money)
CREATE TABLE invoices (
    id TEXT PRIMARY KEY,               -- "inv_2026_001"
    branch_id TEXT NOT NULL,
    project_id TEXT,                   -- Link to Project (Optional, could be quick sale)
    client_id TEXT NOT NULL,
    
    invoice_number TEXT NOT NULL,      -- "BLR-2026-001" (Sequential per branch)
    
    -- Amounts
    subtotal REAL NOT NULL,            -- Sum of line items
    tax_total REAL DEFAULT 0,          -- GST/VAT
    discount_total REAL DEFAULT 0,
    grand_total REAL NOT NULL,         -- The final amount to pay
    
    balance_due REAL NOT NULL,         -- grand_total - paid_amount
    status TEXT DEFAULT 'draft',       -- "draft", "sent", "partial", "paid", "void"
    
    -- Snapshot (JSON) of Line Items to prevent history changing if price changes later
    -- [{ "desc": "Wedding Shoot", "qty": 1, "rate": 50000, "tax": 18 }]
    line_items_json TEXT NOT NULL, 
    
    due_date INTEGER,
    created_at INTEGER DEFAULT (unixepoch()),
    
    FOREIGN KEY (branch_id) REFERENCES branches(id)
);

-- B. Transactions (The Actual Money Movement)
CREATE TABLE transactions (
    id TEXT PRIMARY KEY,               -- "txn_razorpay_123"
    branch_id TEXT NOT NULL,
    invoice_id TEXT NOT NULL,
    
    amount REAL NOT NULL,
    method TEXT NOT NULL,              -- "upi", "card", "cash", "bank_transfer"
    
    -- Gateway Metadata
    gateway_id TEXT,                   -- Razorpay Payment ID
    gateway_status TEXT,               -- "captured", "failed"
    
    -- The Split (Nodal Account Logic)
    platform_fee REAL DEFAULT 0,       -- Our Cut
    net_amount REAL DEFAULT 0,         -- User's Cut
    
    payment_date INTEGER DEFAULT (unixepoch()),
    created_by_user_id TEXT,           -- If Cash, who collected it?
    
    FOREIGN KEY (invoice_id) REFERENCES invoices(id)
);

-- C. Wallet_Ledger (The Virtual Bank)
-- Tracks the User's Earnings/Withdrawals
CREATE TABLE wallet_ledger (
    id TEXT PRIMARY KEY,
    org_id TEXT NOT NULL,
    
    type TEXT NOT NULL,                -- "credit" (Sale), "debit" (Withdrawal/Fee)
    amount REAL NOT NULL,
    description TEXT,                  -- "Sale: Invoice #001" or "Withdrawal to HDFC"
    
    reference_id TEXT,                 -- Link to transaction_id or withdrawal_request_id
    running_balance REAL NOT NULL,     -- The balance AFTER this row
    
    created_at INTEGER DEFAULT (unixepoch())
);

-- INDEXES
CREATE INDEX idx_invoices_status ON invoices(branch_id, status);
CREATE INDEX idx_transactions_inv ON transactions(invoice_id);
CREATE INDEX idx_wallet_org ON wallet_ledger(org_id, created_at);
```