# Lifecycle Events & Data Retention

## 1. Downgrade Logic (The "Overage" Trap)
* **Scenario:** User has 60GB used (Paid Plan) -> Downgrades to Free (2GB limit).
* **Immediate State:** Account marked `Over_Limit`.
* **Consequences:**
    1.  **Upload Block:** No new files can be uploaded.
    2.  **Client Lock:** Client Portals for *old* projects are paused (Client sees: "Gallery Temporarily Unavailable").
    3.  **Grace Period:** User has 14 days to delete 58GB of data.

## 2. Deletion & Archival
* **Manual:** User selects "Delete Project".
    * *Safety:* Moved to "Trash" for 30 days (Recoverable). Then Hard Delete.
* **Auto-Delete Timer:**
    * Feature: User sets "Auto-delete Raw files 6 months after Project Completion".
    * System executes delete to free up space/stop billing.

## 3. Wallet Refunds
* **Rule:** "Promo Credits" (Cashback) are **Non-Refundable**.
* **Rule:** "Real Cash" (Top-ups/Earnings) are **Withdrawable**.
* **Process:** User requests refund -> Admin Approval -> Processed to Bank via Nodal Account.