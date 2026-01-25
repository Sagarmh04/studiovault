# Offline Sync Architecture (Web & Desktop)

## 1. The Strategy: "Local First, Cloud Truth"
* **Web App:** Always Live (Talks to Cloudflare Workers).
* **Desktop App:** Local First (Talks to local SQLite).

## 2. The Data Flow (Desktop)
1.  **Read:** Application reads strictly from local SQLite file.
2.  **Write:** Application writes to local SQLite + adds entry to `sync_queue` table.
3.  **Background Process:**
    * Checks Internet connection.
    * **PUSH:** Sends `sync_queue` items to Cloudflare Worker API.
    * **PULL:** Asks API for "All changes since `last_sync_timestamp`".
    * **MERGE:** Updates local SQLite with Cloudflare data.

## 3. Conflict Resolution
* **Scenario:** User A (Offline) edits Project X. User B (Online) deletes Project X.
* **Strategy:** "Server Wins" (Default).
    * When User A comes online, their edit is rejected by the API because Project X no longer exists.
    * UI shows a "Conflict/Error" notification to User A.

## 4. Initial Setup (On Install)
* Desktop App downloads a compressed SQLite dump (Snapshot) from R2 for the specific Branch.
* Rehydrates the local DB.
* Starts Syncing from the Snapshot Timestamp.