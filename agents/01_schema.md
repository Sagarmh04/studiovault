
# StudioVault D1 Schema

This file contains the complete SQL schema for the StudioVault application, extracted from the PRD.

## 1. Identity Layer Tables

### organizations
```sql
CREATE TABLE organizations (
  id TEXT PRIMARY KEY,
  name TEXT NOT NULL,
  config_json TEXT,
  plan_tier TEXT,
  created_at INTEGER,
  version INTEGER DEFAULT 1
);
```

### branches
```sql
CREATE TABLE branches (
  id TEXT PRIMARY KEY,
  org_id TEXT NOT NULL REFERENCES organizations(id),
  name TEXT NOT NULL,
  address_json TEXT,
  tax_json TEXT,
  invoice_prefix TEXT,
  created_at INTEGER,
  version INTEGER DEFAULT 1
);
CREATE INDEX idx_branches_org_id ON branches(org_id);
```

### users
```sql
CREATE TABLE users (
  id TEXT PRIMARY KEY,
  org_id TEXT NOT NULL REFERENCES organizations(id),
  branch_id TEXT REFERENCES branches(id),
  email TEXT UNIQUE,
  roles_json TEXT,
  status TEXT,
  created_at INTEGER,
  version INTEGER DEFAULT 1
);
CREATE INDEX idx_users_org_id ON users(org_id);
CREATE INDEX idx_users_branch_id ON users(branch_id);
```

## 2. CRM & Client Tables

### clients
```sql
CREATE TABLE clients (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  name TEXT NOT NULL,
  phone TEXT NOT NULL,
  profile_json TEXT,
  total_spend REAL DEFAULT 0,
  created_at INTEGER,
  version INTEGER DEFAULT 1
);
CREATE INDEX idx_clients_branch_id_phone ON clients(branch_id, phone);
CREATE INDEX idx_clients_branch_id_name ON clients(branch_id, name);
```

## 3. Project & Booking Tables

### projects
```sql
CREATE TABLE projects (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  client_id TEXT NOT NULL REFERENCES clients(id),
  status TEXT NOT NULL,
  start_date INTEGER,
  details_json TEXT,
  activated_at INTEGER,
  created_at INTEGER,
  version INTEGER DEFAULT 1
);
CREATE INDEX idx_projects_branch_id_status ON projects(branch_id, status);
CREATE INDEX idx_projects_branch_id_start_date ON projects(branch_id, start_date);
CREATE INDEX idx_projects_client_id ON projects(client_id);
```

### packages
```sql
CREATE TABLE packages (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  name TEXT NOT NULL,
  type TEXT,
  price REAL NOT NULL,
  tax_rate REAL NOT NULL,
  inclusions_json TEXT,
  exclusions_json TEXT,
  resource_hooks_json TEXT,
  version INTEGER DEFAULT 1
);
CREATE INDEX idx_packages_branch_id ON packages(branch_id);
```

## 4. Inventory & Resource Tables

### assets
```sql
CREATE TABLE assets (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  type TEXT NOT NULL,
  name TEXT NOT NULL,
  serial_number TEXT,
  status TEXT NOT NULL,
  metadata_json TEXT,
  version INTEGER DEFAULT 1
);
CREATE INDEX idx_assets_branch_id_status ON assets(branch_id, status);
CREATE INDEX idx_assets_branch_id_serial_number ON assets(branch_id, serial_number);
```

## 5. Media & Storage Tables

### media_objects
```sql
CREATE TABLE media_objects (
  id TEXT PRIMARY KEY,
  project_id TEXT NOT NULL REFERENCES projects(id),
  branch_id TEXT NOT NULL REFERENCES branches(id),
  path TEXT NOT NULL,
  file_type TEXT,
  size_bytes INTEGER NOT NULL,
  watermark_state TEXT,
  uploaded_at INTEGER,
  version INTEGER DEFAULT 1
);
CREATE INDEX idx_media_objects_project_id ON media_objects(project_id);
CREATE INDEX idx_media_objects_branch_id ON media_objects(branch_id);
```

## 6. Finance Tables (Invoice-Based)

### invoices
```sql
CREATE TABLE invoices (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  project_id TEXT REFERENCES projects(id),
  invoice_type TEXT,
  amount_total REAL NOT NULL,
  tax_json TEXT,
  status TEXT NOT NULL,
  issued_at INTEGER,
  due_at INTEGER,
  version INTEGER DEFAULT 1
);
CREATE INDEX idx_invoices_branch_id_status ON invoices(branch_id, status);
CREATE INDEX idx_invoices_project_id ON invoices(project_id);
```

### transactions
```sql
CREATE TABLE transactions (
  id TEXT PRIMARY KEY,
  invoice_id TEXT NOT NULL REFERENCES invoices(id),
  gateway_payment_id TEXT NOT NULL,
  status TEXT NOT NULL,
  amount REAL NOT NULL,
  created_at INTEGER
);
CREATE INDEX idx_transactions_invoice_id ON transactions(invoice_id);
CREATE INDEX idx_transactions_gateway_payment_id ON transactions(gateway_payment_id);
```

## 7. Communication Tables

### messages
```sql
CREATE TABLE messages (
  id TEXT PRIMARY KEY,
  scope_type TEXT,
  scope_id TEXT NOT NULL,
  sender_user_id TEXT NOT NULL REFERENCES users(id),
  content TEXT,
  attachments_json TEXT,
  created_at INTEGER
);
CREATE INDEX idx_messages_scope ON messages(scope_type, scope_id);
```

### notifications
```sql
CREATE TABLE notifications (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  project_id TEXT REFERENCES projects(id),
  type TEXT NOT NULL,
  channel TEXT NOT NULL,
  cost REAL DEFAULT 0,
  billed BOOLEAN DEFAULT 0,
  created_at INTEGER
);
CREATE INDEX idx_notifications_branch_id ON notifications(branch_id);
CREATE INDEX idx_notifications_project_id ON notifications(project_id);
```

## 8. Governance & Audit Tables

### audit_logs
```sql
CREATE TABLE audit_logs (
  id TEXT PRIMARY KEY,
  org_id TEXT NOT NULL REFERENCES organizations(id),
  branch_id TEXT REFERENCES branches(id),
  actor_user_id TEXT NOT NULL REFERENCES users(id),
  event_type TEXT NOT NULL,
  severity TEXT,
  payload_json TEXT,
  created_at INTEGER
);
CREATE INDEX idx_audit_logs_org_id_created_at ON audit_logs(org_id, created_at);
CREATE INDEX idx_audit_logs_branch_id_created_at ON audit_logs(branch_id, created_at);
CREATE INDEX idx_audit_logs_event_type ON audit_logs(event_type);
```
