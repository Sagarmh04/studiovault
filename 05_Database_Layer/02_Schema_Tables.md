Schema Tables (Canonical Phase 1 Database)

StudioVault uses Cloudflare D1 (SQLite) with Drizzle ORM.

This file defines the authoritative table set for Phase 1.

Rules:
- All IDs are TEXT (CUID/UUID style) for sharding simplicity
- All mutable tables include optimistic locking via `version`
- JSON fields are used for flexible configs without schema fatigue

---

## 1. Identity Layer Tables

### organizations
Tenant root entity.

Columns:
- id TEXT PRIMARY KEY
- name TEXT NOT NULL
- config_json TEXT            -- branding, currency, feature toggles
- plan_tier TEXT             -- free_org, paid_org
- created_at INTEGER
- version INTEGER DEFAULT 1

---

### branches
Operational unit (billing + workflow scope).

Columns:
- id TEXT PRIMARY KEY
- org_id TEXT NOT NULL REFERENCES organizations(id)
- name TEXT NOT NULL
- address_json TEXT
- tax_json TEXT              -- GST/VAT identity
- invoice_prefix TEXT        -- BLR-, MUM-
- created_at INTEGER
- version INTEGER DEFAULT 1

Indexes:
- (org_id)

---

### users
Staff identities (Firebase UID aligned).

Columns:
- id TEXT PRIMARY KEY         -- Firebase UID
- org_id TEXT NOT NULL REFERENCES organizations(id)
- branch_id TEXT REFERENCES branches(id)
- email TEXT UNIQUE
- roles_json TEXT             -- ["owner","manager"]
- status TEXT                 -- active, suspended
- created_at INTEGER
- version INTEGER DEFAULT 1

Indexes:
- (org_id)
- (branch_id)

---

## 2. CRM & Client Tables

### clients
Branch-scoped customer database.

Columns:
- id TEXT PRIMARY KEY
- branch_id TEXT NOT NULL REFERENCES branches(id)
- name TEXT NOT NULL
- phone TEXT NOT NULL
- profile_json TEXT           -- address, GST, notes
- total_spend REAL DEFAULT 0
- created_at INTEGER
- version INTEGER DEFAULT 1

Indexes:
- (branch_id, phone)
- (branch_id, name)

---

## 3. Project & Booking Tables

### projects
The main workflow container.

Columns:
- id TEXT PRIMARY KEY
- branch_id TEXT NOT NULL REFERENCES branches(id)
- client_id TEXT NOT NULL REFERENCES clients(id)
- status TEXT NOT NULL        -- inquiry, active, shooting, editing, completed, archived
- start_date INTEGER
- details_json TEXT           -- dynamic project metadata
- activated_at INTEGER        -- when counts toward caps
- created_at INTEGER
- version INTEGER DEFAULT 1

Indexes:
- (branch_id, status)
- (branch_id, start_date)
- (client_id)

---

### packages
Sellable services (branch-local copy).

Columns:
- id TEXT PRIMARY KEY
- branch_id TEXT NOT NULL REFERENCES branches(id)
- name TEXT NOT NULL
- type TEXT                   -- time_based, qty_based
- price REAL NOT NULL
- tax_rate REAL NOT NULL
- inclusions_json TEXT
- exclusions_json TEXT
- resource_hooks_json TEXT
- version INTEGER DEFAULT 1

Indexes:
- (branch_id)

---

## 4. Inventory & Resource Tables

### assets
Bookable gear/spaces.

Columns:
- id TEXT PRIMARY KEY
- branch_id TEXT NOT NULL REFERENCES branches(id)
- type TEXT NOT NULL          -- camera, lens, space, human
- name TEXT NOT NULL
- serial_number TEXT
- status TEXT NOT NULL        -- available, booked, maintenance, lost
- metadata_json TEXT
- version INTEGER DEFAULT 1

Indexes:
- (branch_id, status)
- (branch_id, serial_number)

---

## 5. Media & Storage Tables

### media_objects
Logical file records (R2 truth source).

Columns:
- id TEXT PRIMARY KEY
- project_id TEXT NOT NULL REFERENCES projects(id)
- branch_id TEXT NOT NULL REFERENCES branches(id)
- path TEXT NOT NULL
- file_type TEXT              -- proxy, raw, delivery, ingest
- size_bytes INTEGER NOT NULL
- watermark_state TEXT        -- proof, clean
- uploaded_at INTEGER
- version INTEGER DEFAULT 1

Indexes:
- (project_id)
- (branch_id)

---

## 6. Finance Tables (Invoice-Based)

### invoices
Billing artifact for projects, POS, subscriptions.

Columns:
- id TEXT PRIMARY KEY
- branch_id TEXT NOT NULL REFERENCES branches(id)
- project_id TEXT REFERENCES projects(id)
- invoice_type TEXT           -- booking, pos, subscription, overage
- amount_total REAL NOT NULL
- tax_json TEXT
- status TEXT NOT NULL        -- draft, issued, paid, overdue
- issued_at INTEGER
- due_at INTEGER
- version INTEGER DEFAULT 1

Indexes:
- (branch_id, status)
- (project_id)

---

### transactions
Immutable payment gateway events.

Columns:
- id TEXT PRIMARY KEY
- invoice_id TEXT NOT NULL REFERENCES invoices(id)
- gateway_payment_id TEXT NOT NULL
- status TEXT NOT NULL        -- paid, refunded, disputed, failed
- amount REAL NOT NULL
- created_at INTEGER

Indexes:
- (invoice_id)
- (gateway_payment_id)

---

## 7. Communication Tables

### messages
Scoped chat records.

Columns:
- id TEXT PRIMARY KEY
- scope_type TEXT             -- lead, project
- scope_id TEXT NOT NULL      -- Lead_ID or Project_ID
- sender_user_id TEXT NOT NULL REFERENCES users(id)
- content TEXT
- attachments_json TEXT
- created_at INTEGER

Indexes:
- (scope_type, scope_id)

---

### notifications
Outbound transactional events.

Columns:
- id TEXT PRIMARY KEY
- branch_id TEXT NOT NULL REFERENCES branches(id)
- project_id TEXT REFERENCES projects(id)
- type TEXT NOT NULL          -- booking_confirmed, invoice_due, photos_ready
- channel TEXT NOT NULL       -- whatsapp, sms, email
- cost REAL DEFAULT 0
- billed BOOLEAN DEFAULT 0
- created_at INTEGER

Indexes:
- (branch_id)
- (project_id)

---

## 8. Governance & Audit Tables

### audit_logs
Immutable high-risk event log.

Columns:
- id TEXT PRIMARY KEY
- org_id TEXT NOT NULL REFERENCES organizations(id)
- branch_id TEXT REFERENCES branches(id)
- actor_user_id TEXT NOT NULL REFERENCES users(id)
- event_type TEXT NOT NULL
- severity TEXT              -- high, medium
- payload_json TEXT
- created_at INTEGER

Indexes:
- (org_id, created_at)
- (branch_id, created_at)
- (event_type)

---

## 9. Enforcement Notes

- No wallet_balance tables exist
- No withdrawal tables exist
- All billing is invoice-based
- Storage usage is computed from media_objects size_bytes truth

---

## 10. Phase 2 Extensions (Not Included Yet)

Deferred tables:
- marketing_campaigns
- vendor_invoices
- video_version_stacks
- approval_requests

## ID Generation Doctrine (Offline-Safe)

All entity IDs are generated client-side using UUID v7.

Format:
- `prj_<uuidv7>
- `inv_<uuidv7>
- `cli_<uuidv7>

Reason:
- Desktop must create records offline
- No server round-trip required
- IDs remain time-sortable and collision-free

Cloud accepts IDs as submitted.
