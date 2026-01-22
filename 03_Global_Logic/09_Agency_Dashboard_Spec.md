# Agency Branch Dashboard (The Pro Interface)

## 1. Context
* **User:** Branch Manager (Agency Mode).
* **Difference from Atomic:** Atomic is about "My Day"; Agency is about "My Operation".
* **Layout:** Sidebar Navigation with distinct "Enterprise Tabs".

## 2. The Logistics Tab (Supply Chain)
* **Goal:** Manage incoming/outgoing gear without calling HQ.
* **Interface:** Two Split Panes.
    * **Incoming (In-Transit):** List of items sent from other branches.
        * *Action:* `Receive` (Scans item into local Inventory).
    * **Outgoing (Dispatched):** List of items sent to others.
        * *Action:* `Recall` (Requests return) or `Mark Lost`.
* **Quick Transfer:** "Send Item" button -> Select Branch -> Select Gear -> Confirm.

## 3. The Library Tab (Global Packages)
* **Goal:** Import standardize services.
* **Views:**
    * **My Packages:** Active services sold at this branch.
    * **Global Library:** Master templates from HQ.
* **Sync Indicators:**
    * `Green Check`: Synced with Master.
    * `Yellow Badge`: "Update Available" (Master has changed).
    * *Action:* Click to review diff -> Apply Update.

## 4. The Audit Tab (Branch Level)
* **Goal:** Local accountability.
* **Scope:** Shows ONLY events triggered within *this specific branch*.
* **Filters:** User (Staff Name), Severity (High/Low), Type (Finance/Ops).
* **Constraint:** Read-Only. No deletion allowed.

## 5. The Production Tab (Kanban)
* **Visual:** Drag-and-drop board for Project Status.
* **Lanes:** `Pre-Production` -> `Shoot` -> `Post-Processing` -> `Review` -> `Completed`.
* **Integration:** Dragging a card updates the `Project_Status` in the database and triggers Client Notifications.