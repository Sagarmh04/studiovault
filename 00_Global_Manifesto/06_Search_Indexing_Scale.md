Search, Indexing & Scale Policy (The Retrieval Spine)

Studios do not browse software.
They search names, phone numbers, dates, and jobs at speed.

Search is not a feature.
Search is the operating system.

---

## 1. Core Principle

If a receptionist cannot find a client in under 2 seconds,
StudioVault fails as studio infrastructure.

Search must be:

- Fast
- Scoped (branch-safe)
- Predictable
- Index-backed (never full-table scans)

---

## 2. Primary Search Entities (Phase 1 Required)

StudioVault must support instant lookup for:

1. Clients
- Name
- Phone number (most common POS key)
- Optional GST / Business name

2. Projects
- Client name association
- Status (Inquiry, Shooting, Editing, Completed)
- Date range filters

3. Inventory Assets
- Serial number
- Name/type (Sony A7iii, Godox Light)

4. Staff & Vendors
- Name lookup
- Assignment visibility

---

## 3. Scope Enforcement (No Global Leakage)

Search is always scope-limited by default:

- Branch search → Branch_ID filtered
- Organization search → Requires explicit HQ privileges

Rule:
No staff member should discover another branch’s client list by searching.

Global client search requires Owner toggle:
"Global Client List Enabled"

---

## 4. Database Indexing Rules (D1 / SQLite)

Phase 1 indexing requirements:

### Clients Table
Indexes:
- (branch_id, phone)
- (branch_id, name)

Phone lookup must be O(log n), not O(n).

### Projects Table
Indexes:
- (branch_id, status)
- (branch_id, start_date)
- (client_id)

### Assets Table
Indexes:
- (branch_id, serial_number)
- (status)

### Users Table
Indexes:
- (org_id, email)

---

## 5. Search UX Standards

Search must support:

- Prefix typing ("Sha…" → Sharma)
- Phone partial match ("98…" → clients)
- Status filters ("Active only")
- Date quick filters ("This Week Shoots")

Reception workflows require single-bar global search.

---

## 6. Performance Guardrails

Phase 1 hard limits:

- Client search results return <200ms at 50k clients/branch
- Project dashboards must paginate, never load-all
- Full-text search beyond name/phone is deferred

Heavy analytics queries must run asynchronously or cached.

---

## 7. Future Scale Extensions (Phase 2+)

When tenant size exceeds SQLite comfort:

Enterprise upgrades may include:

- Dedicated per-tenant databases
- Full-text search engines (Meilisearch / Elastic)
- Global analytics warehouse layer

Search evolution is driven by real branch scale, not premature complexity.

---

## 8. Trust Rule

Studios trust software that remembers.

Search is memory.
Indexing is discipline.
Scale is survival.
