Audit Log Schema (The Immutable Truth Ledger)

StudioVault operates in domains where trust is expensive:

- Money
- Contracts
- Client data
- Multi-staff operations

Audit logs are the platform’s legal memory.

They are immutable.
They are scoped.
They are non-negotiable.

---

## 1. Core Principle

Audit logs are not analytics.

Audit logs are for:

- Fraud investigation
- Compliance traceability
- Governance enforcement
- Accountability across branches

Rule:
Audit events cannot be edited or deleted.

---

## 2. What Gets Logged (High-Risk Actions Only)

To avoid noise, StudioVault logs only critical actions:

### Financial Events
- Refund initiation
- Refund approval/rejection
- Invoice voiding/deletion
- Discounts above threshold

### Operational Events
- Project deletion (trash + hard delete)
- Asset marked Lost/Stolen
- Branch-level package overrides

### Security Events
- Role changes
- Failed login spikes
- Client export actions

### Governance Events
- Approval requests
- Owner overrides
- Policy threshold changes

---

## 3. Canonical Table: audit_logs

Each audit entry is a single immutable event.

Columns:

- id TEXT PRIMARY KEY
- org_id TEXT NOT NULL
- branch_id TEXT NULLABLE
- actor_user_id TEXT NOT NULL

- event_type TEXT NOT NULL
  Examples:
  - refund_requested
  - refund_approved
  - project_deleted
  - role_changed
  - export_triggered

- severity TEXT NOT NULL
  Values:
  - high
  - medium

- payload_json TEXT NOT NULL
  Contains structured context:
  - affected entity_id
  - before/after snapshots (minimal)
  - approval notes
  - gateway references

- created_at INTEGER NOT NULL

Indexes:
- (org_id, created_at)
- (branch_id, created_at)
- (event_type)

---

## 4. Visibility & Access Scope

Audit visibility is role-scoped:

### Branch Manager
- Can view only branch-linked audit events
- Cannot view HQ or other branches

### Organization Owner / HQ
- Can view all org-wide events
- Can filter by branch, user, severity

Audit logs are always read-only.

---

## 5. Retention Policy

Default retention:

- Free tier: 90 days rolling
- Paid extensions:
  - 1 year
  - 3 years
  - Forever (enterprise compliance add-on)

Logs older than retention are auto-purged
except where legal retention requires otherwise.

---

## 6. Audit Integrity Rules

- Audit events are append-only
- No UPDATE or DELETE operations allowed
- Events are written server-side only
- Client cannot forge audit history

All enforcement actions must emit an audit event.

---

## 7. Example Event Payloads

Refund Approved:

{
  "invoice_id": "inv_123",
  "amount": 20000,
  "approver": "usr_owner",
  "reason": "Client cancellation",
  "gateway_ref": "pay_xyz"
}

Client Export Triggered:

{
  "export_type": "client_list_csv",
  "initiated_by": "usr_owner",
  "ip_address": "masked"
}

---

## 8. Doctrine

Audit logs are the platform’s conscience.

Without audit:
- governance is theater
- compliance is fiction
- trust is impossible
