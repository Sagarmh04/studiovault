Sharding & Tenant Database Strategy (The Scale Partition Doctrine)

StudioVault is multi-tenant by default.

To stay cost-efficient while supporting enterprise scale,
the data layer must support controlled partitioning.

This document defines the canonical tenant database strategy.

---

## 1. Core Principle

Small studios should not pay enterprise infrastructure costs.

Enterprise agencies must not share performance or risk boundaries.

Therefore:

- Default = Shared Database
- Upgrade path = Dedicated Database

---

## 2. Phase 1 Model: Sharded Multi-Tenant SQLite (D1)

StudioVault uses Cloudflare D1 (SQLite) with logical tenant isolation.

Default Deployment:
- Multiple small branches coexist in a shared D1 database

Isolation Rule:
- Every query is scoped by branch_id (and org_id where required)

Cross-tenant leakage is treated as a SEV1 security breach.

---

## 3. Tenant Classes

### Class A: Shared Tenants (Default)

Applies to:
- Free studios
- Pro studios under scale threshold

Characteristics:
- Shared DB instance
- Strict branch/org scoping
- Cost-efficient hosting

---

### Class B: Dedicated Tenants (Enterprise)

Applies when:
- Client volume exceeds SQLite comfort
- Media metadata volume becomes extreme
- Enterprise compliance requires isolation

Dedicated DB guarantees:
- Performance isolation
- Operational safety boundary
- Custom retention + audit extensions

---

## 4. Scale Threshold Triggers (Migration Criteria)

Dedicated database eligibility may trigger at:

- >200k clients per branch
- >1M media_objects rows per tenant
- Heavy analytics load (Agency dashboards)
- Enterprise contract requiring isolation

Thresholds are operational, not arbitrary.

---

## 5. Migration Strategy (No Downtime Goal)

Migration is executed as:

1. Snapshot Export
- Tenant data exported from shared shard

2. Dedicated DB Provision
- New D1 database created for tenant

3. Dual-Write Window (Optional Phase 2)
- Writes mirrored briefly for safety

4. Cutover
- Tenant routing updated to dedicated DB

5. Verification
- Checksums + row counts validated

Tenant migration is an Owner-visible governance event.

---

## 6. Routing Layer (Database Resolver)

All API calls resolve database via:

- org_id → shard assignment
- branch_id → tenant database mapping

No direct DB addressing exists in client code.

This allows invisible scaling without UX disruption.

---

## 7. Governance Constraints

Branch managers cannot:
- See shard assignments
- Switch tenants
- Export other tenant data

Only HQ system operators can migrate tenants.

All migrations are audit-logged.

---

## 8. Future Phase Resilience (Phase 2+)

Enterprise-grade expansions:

- Multi-region replication for dedicated tenants
- Read replicas for analytics workloads
- Tiered archival databases for completed projects

---

## 9. Doctrine

Shared databases buy affordability.
Dedicated databases buy sovereignty.

Sharding is how StudioVault scales without losing simplicity.
