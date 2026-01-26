# Flaw 7: Status Fields Need Enums or Constraints

## User Feedback
A major risk in the initial schema was the use of loose `TEXT` fields for status columns (`projects.status`, `invoices.status`, etc.). This allows for typos and inconsistent data, which can break workflows and corrupt state management. The recommendation was to use `CHECK` constraints to enforce a strict set of allowed values, similar to an enum.

## Resolution
To drastically improve data integrity, I am implementing `CHECK` constraints on all relevant status fields. Because SQLite does not support adding constraints to existing tables, and these tables have multiple dependencies, the most robust solution is to drop all existing tables and recreate them with the corrected, more secure schema.

This change ensures that status fields can only ever contain valid, expected values, preventing a wide class of potential bugs and data corruption issues.

## New Schemas with Constraints

### projects
```sql
CREATE TABLE projects (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  client_id TEXT NOT NULL REFERENCES clients(id),
  status TEXT NOT NULL CHECK (status IN ('inquiry', 'active', 'shooting', 'editing', 'completed', 'archived')),
  start_date INTEGER,
  details_json TEXT,
  activated_at INTEGER,
  created_at INTEGER,
  version INTEGER DEFAULT 1
);
```

### invoices
```sql
CREATE TABLE invoices (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  project_id TEXT REFERENCES projects(id),
  invoice_type TEXT,
  amount_total REAL NOT NULL,
  tax_json TEXT,
  status TEXT NOT NULL CHECK (status IN ('draft', 'issued', 'paid', 'overdue')),
  issued_at INTEGER,
  due_at INTEGER,
  version INTEGER DEFAULT 1
);
```

### transactions
```sql
CREATE TABLE transactions (
  id TEXT PRIMARY KEY,
  invoice_id TEXT NOT NULL REFERENCES invoices(id),
  gateway_payment_id TEXT NOT NULL,
  status TEXT NOT NULL CHECK (status IN ('paid', 'refunded', 'disputed', 'failed')),
  amount REAL NOT NULL,
  created_at INTEGER
);
```

### pos_orders
```sql
CREATE TABLE pos_orders (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  total_amount REAL NOT NULL,
  items_json TEXT NOT NULL,
  payment_method TEXT,
  status TEXT NOT NULL CHECK (status IN ('paid', 'voided', 'corrected')),
  created_at INTEGER NOT NULL
);
```
