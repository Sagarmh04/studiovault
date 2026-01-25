Core Entities (The Data Map of StudioVault)

StudioVault is a Studio Operating System.
All features reduce to a small set of canonical entities.

This file defines the official object model of the platform.
Engineering treats this as the single source of truth.

---

## 1. Tenant Hierarchy (Identity Spine)

### Organization (Tenant)
The legal business entity.

Represents:
- Brand ownership
- Subscription ownership
- Global governance layer

Key Properties:
- name
- billing_plan (free/org-paid)
- global_settings_json
- policy toggles (global client list, approval caps)

Relationship:
- Organization has many Branches

---

### Branch (Operational Unit)
The atomic studio location where work happens.

Represents:
- A physical studio or business unit
- The primary billing unit in Phase 1

Key Properties:
- org_id
- address + tax identity (GST/VAT)
- invoice sequence prefix
- storage usage + quota scope

Relationship:
- Branch has many Projects, Clients, Assets, Users

---

### User (Staff Member)
A human login identity scoped by role.

Key Properties:
- firebase_uid (primary identity)
- role array (RBAC union logic)
- branch assignment (default)

Roles include:
- Owner
- Manager
- Clerk
- Photographer
- Accountant
- Vendor (limited portal)

---

## 2. Client & Revenue Entities

### Client (Customer Record)
A client belongs to a branch by default.

Key Properties:
- name
- phone (primary POS lookup key)
- optional GST + address
- lifetime spend cache

Rules:
- Branch-siloed unless Org explicitly enables sharing

---

### Project (Booking + Delivery Container)
The central operational entity.

Represents:
- A wedding shoot
- A commercial contract
- A post-production workflow container

Key Properties:
- client_id
- branch_id
- status (inquiry, shooting, editing, completed)
- start_date
- details_json (dynamic by project type)

Activation Rule:
- Becomes Active only after acceptance/payment/offline confirmation

Projects are contractual scheduled workflows.  
Walk-in counter transactions are stored separately as POS Orders.


---

### Package (Sellable Service Unit)
Reusable template for quoting.

Types:
- Time-based (Wedding 8 hours)
- Qty-based (Passport photo pack)

Key Properties:
- name
- pricing + tax metadata
- resource hooks (optional)

Inheritance:
- Org master templates → Branch local copies

---

## 3. Scheduling & Operations

### Resource / Asset (Inventory Unit)
Anything that can be booked or locked.

Asset Classes:
- Fixed gear (camera, lens)
- Spaces (studio floor)
- Humans (staff availability)

Key Properties:
- serial_number (for gear)
- status (available, booked, maintenance)

---

### Booking Lock (Conflict Prevention Unit)
Not always a separate table, but a rule:

A Project consumes resources for a time window.
Conflicts reject bookings deterministically.

---

## 4. Financial Entities (Invoice-Based)

### Invoice (Billing Artifact)
StudioVault operates through invoices, not wallets.

Invoices apply to:
- Project bookings
- Walk-in POS orders
- Subscription + overages

Key Properties:
- amount_total
- tax breakdown
- status (draft, issued, paid, overdue)

---

### Transaction (Gateway Event Record)
Immutable payment provider events.

Key Properties:
- gateway_payment_id
- invoice_id
- status (paid, refunded, disputed)
- timestamp

No stored-value wallet balances exist.

---

### Refund / Dispute Case (Governance Unit)
State machine for financial reversals.

States:
- Paid → Disputed → Under Review → Resolved (Won/Lost)

Governance:
- Owner-only initiation
- Threshold approval enforcement

---

## 5. Media & Storage Entities

### Media Object (File Record)
Stored in Cloudflare R2.

Types:
- Proxy preview
- RAW originals (Pro tier)
- Delivery exports
- Vendor ingest uploads

Key Properties:
- project_id
- path + size_bytes
- visibility + watermark state

Quota Enforcement:
- Storage usage billed monthly

---

## 6. Communication Entities

### Message (Scoped Chat Unit)
Messages exist only inside contexts:

- Lead Chat (pre-booking)
- Project Chat (post-booking)

Key Properties:
- scope_id
- sender_id
- content + attachments

---

### Notification Event
Transactional outbound messages:

- Booking confirmed
- Payment reminder
- Photos ready

Key Properties:
- type
- delivery channel (WhatsApp/SMS/Email)
- billed_overage flag

---

## 7. Governance & Audit

### Audit Log Event (Immutable Record)
High-risk actions only.

Triggers:
- Refund approval
- Invoice voiding
- Role change
- Project deletion

Retention:
- Free: 90 days
- Paid: extendable

Audit logs cannot be edited or deleted.

---

## 8. Cross-Cutting Doctrine

Everything in StudioVault reduces to:

Identity → Projects → Media → Money → Trust

If an entity is not in this file,
it is not considered canonical until added here.
