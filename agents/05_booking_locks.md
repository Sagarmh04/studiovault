# Flaw 5: Missing Booking Locks for Resource Conflicts

## User Feedback
The PRD states a hard rule that resources (assets) must be locked for specific time windows to prevent double bookings. The initial schema, however, was missing a `booking_locks` table, leaving this critical rule purely conceptual and unenforceable at the database level.

## Resolution
To implement the resource locking mechanism, I am adding a new `booking_locks` table. This table creates an explicit link between a project, an asset, and a time window (`start_time`, `end_time`).

The index `idx_booking_locks_asset_time` is crucial here, as it allows for efficient querying to detect and prevent conflicting bookings for the same asset at the same time. This table provides the source of truth for resource availability.

## Schema
```sql
CREATE TABLE booking_locks (
  id TEXT PRIMARY KEY,
  project_id TEXT NOT NULL REFERENCES projects(id),
  asset_id TEXT NOT NULL REFERENCES assets(id),
  start_time INTEGER NOT NULL,
  end_time INTEGER NOT NULL,
  created_at INTEGER NOT NULL
);
CREATE INDEX idx_booking_locks_asset_time
  ON booking_locks(asset_id, start_time, end_time);
```
