Backup & Disaster Recovery (The Memory Covenant)

StudioVault stores irreplaceable client work (weddings, commercial shoots, life events).
Data loss is not a bug — it is existential failure.

This document defines the minimum safety guarantees of the platform.

---

## 1. Core Principle

StudioVault is not a “file host.”
It is a professional archive system.

Therefore:

- Media must be durable
- Metadata must be recoverable
- Deletion must be reversible (within policy windows)
- Disaster recovery must be tested, not assumed

---

## 2. Data Classes & Risk Levels

StudioVault stores multiple categories of data:

1. Metadata (Critical)
- Clients, Projects, Bookings, Invoices, Contracts
- Stored in Cloudflare D1

2. Media Assets (High Value)
- Photos, videos, proxies, RAW originals (Pro)
- Stored in Cloudflare R2

3. Audit Logs (Compliance)
- Security events, approvals, refunds
- Stored with retention policies

---

## 3. Backup Strategy (Phase 1)

### A) Database Backups (D1)

Frequency:
- Daily automated snapshots

Retention:
- 7 days rolling (Free/Standard)
- Extendable in enterprise tiers

Recovery Objective:
- RPO (Recovery Point Objective): ≤ 24 hours
- RTO (Recovery Time Objective): ≤ 4 hours for critical restore

Notes:
- Snapshots are stored in isolated backup storage
- Restore requires Org Owner authorization

---

### B) Media Durability (R2)

Cloudflare R2 provides high durability storage by default.

Additional Safeguards:
- Object versioning (future scope)
- Lifecycle rules for archival tiers

Media Recovery Rules:
- Deleted project media enters Trash window before hard delete
- No instant destructive deletes without recoverability period

---

## 4. Deletion Safety Model

StudioVault enforces a two-step deletion policy:

1. Soft Delete (Trash)
- Project moved into Trash for 30 days
- Fully recoverable by Owner/Admin

2. Hard Delete
- Executed only after Trash expiry
- Media + metadata permanently removed

This prevents accidental loss.

---

## 5. Non-Payment & Export Safeguards

If an account becomes overdue:

- Grace period: 7 days
- Delivery portal frozen after grace
- Uploads blocked

Final Safeguards:
- Day 45: Final warning sent
- Day 45: One-click Export ZIP offered
- Day 60: Storage eligible for deletion if unpaid

StudioVault guarantees users can retrieve data before enforcement deletion.

---

## 6. Disaster Scenarios & Response

### Scenario A: Database Corruption / D1 Failure
Response:
- Restore most recent snapshot
- Replay transaction logs where possible

### Scenario B: Accidental Project Deletion
Response:
- Recover from Trash within 30 days

### Scenario C: R2 Object Loss / Provider Outage
Response:
- Platform enters read-only mode
- Recovery executed via provider redundancy + backups (Phase 2 multi-region)

---

## 7. Operational Testing (Required)

Disaster Recovery is not theoretical.

Minimum Requirements:
- Quarterly restore drills (internal)
- Backup verification checksums
- Incident log + postmortems

---

## 8. Future Scope (Phase 2 Resilience Moats)

- Multi-region replication for enterprise tiers
- Customer-managed backup export automation
- Immutable storage for legal archives
- Object-level version rollback for RAW libraries

---

## 9. Trust Contract

StudioVault exists to protect memories and revenue.

Backup and recovery is not a feature.
It is a covenant.
