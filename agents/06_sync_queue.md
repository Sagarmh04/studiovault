# Flaw 6: Missing Offline Sync Queue Table

## User Feedback
The application is designed to be "desktop-first" and support offline operations. This requires a mechanism to queue changes made offline and sync them with the server later. The initial schema was missing a `sync_queue` table, making the entire offline-first strategy impossible to implement.

## Resolution
To enable offline capabilities, I am introducing a new `sync_queue` table. This table will act as a log of all operations (creates, updates, deletes) that occur while the application is offline.

Each row represents a single action to be performed, with its status tracked in the `sync_status` field. This allows a background process to reliably and idempotently apply these changes to the server once a connection is restored.

## Schema
```sql
CREATE TABLE sync_queue (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL,
  entity_type TEXT NOT NULL,
  operation TEXT NOT NULL,
  payload_json TEXT NOT NULL,
  sync_status TEXT DEFAULT 'pending',
  created_at INTEGER NOT NULL
);
```
