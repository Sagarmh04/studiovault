Offline Sync Model (Local First, Cloud Truth)

StudioVault supports desktop workflows that must function without internet:

- POS Walk-in billing
- Smart Select media bridge
- On-location studio operations

Offline systems require strict sync discipline.

---

## 1. Core Principle

Desktop apps operate as:

- Local First for usability
- Cloud Truth for governance

Rule:
The user experience reads locally.
The platform truth resolves globally.

---

## 2. Local Data Layer (Desktop)

Desktop application maintains:

- Local SQLite database
- Append-only transaction log
- Sync queue table

Writes always succeed locally first.

---

## 3. Sync Queue Architecture

Every offline mutation creates a sync event:

Table: sync_queue

Event contains:
- id
- entity_type (project, invoice, pos_order)
- operation (create, update, void)
- payload_json
- created_at
- sync_status (pending, sent, confirmed, rejected)

This prevents full database scans.

---

## 4. Sync Flow (Push + Pull)

### PUSH (Local → Cloud)

1. Desktop detects connectivity
2. Sends pending sync_queue events to Worker API
3. Server validates:
   - permissions
   - version checks
   - entity existence
4. Server commits change
5. Desktop marks event confirmed

---

### PULL (Cloud → Local)

Desktop requests:

“All changes since last_sync_timestamp”

Server responds with:
- diff events
- updated entities
- deletion markers

Desktop merges into local SQLite.

---

## 5. Conflict Resolution Doctrine

Conflicts are inevitable.

Default Rule:
Server Wins

Scenario:
- User A edits Project X offline
- User B deletes Project X online

Resolution:
- Offline edit rejected on sync
- Desktop shows conflict notification:
  “Project was deleted remotely”

No silent merge ambiguity is allowed.

---

## 6. POS Append-Only Integrity (Critical)

POS and walk-in billing must not rewrite history.

Rule:
Offline POS is append-only.

Corrections are modeled as new events:

- Correction Entry (not overwrite)
- Voided Transaction (logged, not erased)

This prevents reconciliation chaos.

---

## 7. Initial Desktop Bootstrap

On install:

1. Desktop downloads branch snapshot from R2
2. Rehydrates local SQLite
3. Stores snapshot timestamp
4. Begins syncing forward from that point

This avoids cold-start empty state.

---

## 8. Sync Safety Guardrails

- Sync is background, never blocking UI
- Events are idempotent (safe to retry)
- Large payloads are chunked
- Audit logs record sync-critical actions

---

## 9. Future Enhancements (Phase 2)

- Delta compression for very large branches
- Multi-device conflict visualization
- Partial entity locking for high-risk edits

---

## 10. Doctrine

Offline is not “lack of internet.”
Offline is distributed systems.

StudioVault sync is strict, boring, and correct.
