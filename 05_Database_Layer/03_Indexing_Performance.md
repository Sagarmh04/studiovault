Indexing & Performance Guardrails (The No-Full-Scan Law)

StudioVault is a high-frequency retrieval system:

- Receptionists search clients instantly
- Managers filter projects constantly
- Booking locks must be deterministic

Performance is not optional.
It is schema-enforced discipline.

---

## 1. Core Principle

Every user-facing query must be index-backed.

Rule:
If a query cannot use an index, it does not ship.

SQLite/D1 will punish full scans at scale.

---

## 2. Phase 1 Performance Targets

Hard UX targets:

- Client lookup <200ms at 50k clients per branch
- Project dashboard paginated always
- Booking conflict checks <100ms
- No unbounded ORDER BY without index support

---

## 3. Mandatory Index Set (Phase 1)

### Clients (POS Critical)

Problem:
Phone number lookup is the #1 receptionist action.

Indexes:
- CREATE INDEX idx_clients_branch_phone ON clients(branch_id, phone);
- CREATE INDEX idx_clients_branch_name  ON clients(branch_id, name);

Rules:
- All client search must include branch_id filter
- Phone lookup must never scan across branches

---

### Projects (Operational Spine)

Indexes:
- CREATE INDEX idx_projects_branch_status
    ON projects(branch_id, status);

- CREATE INDEX idx_projects_branch_startdate
    ON projects(branch_id, start_date);

- CREATE INDEX idx_projects_client
    ON projects(client_id);

Rules:
- Active project views must filter branch_id + status
- Kanban boards always paginate by lane

---

### Invoices (Billing Visibility)

Indexes:
- CREATE INDEX idx_invoices_branch_status
    ON invoices(branch_id, status);

- CREATE INDEX idx_invoices_project
    ON invoices(project_id);

Rule:
Finance dashboards must never compute totals live via scans.
Use cached summaries if needed.

---

### Transactions (Gateway Traceability)

Indexes:
- CREATE INDEX idx_transactions_invoice
    ON transactions(invoice_id);

- CREATE INDEX idx_transactions_gatewayid
    ON transactions(gateway_payment_id);

Rule:
Chargeback/dispute lookup must be instant.

---

### Media Objects (Storage Quota Truth)

Indexes:
- CREATE INDEX idx_media_project
    ON media_objects(project_id);

- CREATE INDEX idx_media_branch
    ON media_objects(branch_id);

Rule:
Quota computations must aggregate per branch/project only.

---

### Assets (Inventory Locks)

Indexes:
- CREATE INDEX idx_assets_branch_status
    ON assets(branch_id, status);

- CREATE INDEX idx_assets_serial
    ON assets(branch_id, serial_number);

Rule:
Serial search must be O(log n).

---

### Audit Logs (Forensics)

Indexes:
- CREATE INDEX idx_audit_org_time
    ON audit_logs(org_id, created_at);

- CREATE INDEX idx_audit_branch_time
    ON audit_logs(branch_id, created_at);

Rule:
Audit browsing must always filter by scope.

---

## 4. Query Guardrails (Engineering Law)

Forbidden Patterns:

- SELECT * without LIMIT on user-facing endpoints
- ORDER BY created_at without supporting index
- Cross-branch queries without Owner privilege
- Full table scans for dashboards

Required Patterns:

- Always include branch_id in WHERE clause for branch data
- Always paginate lists:
  LIMIT 50 OFFSET n
- Use cursor pagination for large activity feeds

---

## 5. Search Constraints (Phase 1)

Phase 1 search is intentionally minimal:

- Prefix search on client name
- Partial match on phone
- Status + date filters on projects

Deferred:
- Full-text search engine
- Global fuzzy matching
- Cross-org discovery

---

## 6. Scale Strategy Triggers (When SQLite Stops Being Cute)

Enterprise escalation points:

- >200k clients per branch
- >1M media_objects in a single tenant
- Complex analytics requiring warehouse queries

At that point, introduce:

- Dedicated tenant DBs
- External search engine (Meilisearch/Elastic)
- Async reporting layer

---

## 7. Doctrine

Indexes are not optimization.
Indexes are architecture.

The fastest query is the one we never execute.
The second fastest is the one that uses the right index.
