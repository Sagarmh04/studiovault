# Flaw 8: Audit Payload Should Not Be Nullable

## User Feedback
The `audit_logs` table is a critical part of the system's security and integrity. The initial schema allowed `payload_json` and `created_at` to be `NULL`, which violates the doctrine of immutable, complete audit trails. An audit event without a payload or a timestamp is of little value.

## Resolution
To enforce the integrity of the audit log, I am modifying the `audit_logs` table to make the `payload_json` and `created_at` columns `NOT NULL`. This ensures that every audit event captures all necessary information at the time it occurs.

## Schema
```sql
CREATE TABLE audit_logs (
  id TEXT PRIMARY KEY,
  org_id TEXT NOT NULL REFERENCES organizations(id),
  branch_id TEXT REFERENCES branches(id),
  actor_user_id TEXT NOT NULL REFERENCES users(id),
  event_type TEXT NOT NULL,
  severity TEXT,
  payload_json TEXT NOT NULL,
  created_at INTEGER NOT NULL
);
CREATE INDEX idx_audit_logs_org_id_created_at ON audit_logs(org_id, created_at);
CREATE INDEX idx_audit_logs_branch_id_created_at ON audit_logs(branch_id, created_at);
CREATE INDEX idx_audit_logs_event_type ON audit_logs(event_type);
```
