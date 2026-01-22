# Global Command Center (The Organization Dashboard)

## 1. Context & Architecture
* **Scope:** Organization Level (Parent Layer).
* **Behavior:**
    * **Atomic Mode (1 Branch):** Displays stats for the single branch, but maintains the "Global" data structure (ready for expansion).
    * **Agency Mode (Multi-Branch):** Aggregates data across all `Branch_ID`s linked to this `Org_ID`.

## 2. The Currency Engine
* **Selector:** Top-right dropdown (e.g., "View in USD", "View in INR").
* **Data Source:** External API (Fixer.io) -> Cached in DB for 1 hour.
* **Frontend Logic:** Reads strictly from Database Cache. Zero latency.

## 3. The "Big Numbers" (Ticker) with Drill-Down
* **Interaction:** Clicking any metric opens a **Detailed Breakdown Report**.
* **Metrics:**
    1.  **Global Gross Revenue:**
        * *Drill-Down:* Bar chart comparing revenue per Branch.
    2.  **Net Sales:** `Gross - Refunds`.
    3.  **Active Projects:**
        * *Drill-Down:* List of all active jobs sorted by "Due Date".
    4.  **Global Storage:**
        * *Drill-Down:* Pie chart of "Storage used by Branch".

## 4. The "Burn Rate" Widget (Centralized Billing)
* **Location:** Prominent Widget (Top Right).
* **Display:**
    * "Next Invoice Due: [Date]"
    * "Estimated Amount: ₹15,400" (Live calculation of Subscription + Storage Overage).
    * "Org Wallet Balance: ₹5,000".
* **Goal:** Prevents service interruption by keeping the Owner aware of upcoming costs.

## 5. The Problem Feed (Exception Management)
* **Alert Types:** Financial (Overdue Invoices), Operational (Double Bookings), System (Storage Full).
* **Lifecycle Logic (HQ Hide):**
    * **Action:** HQ clicks "Dismiss/Acknowledge".
    * **Result:** Alert disappears from HQ Dashboard **ONLY**.
    * **Constraint:** The alert remains **Active & Red** on the specific Branch Manager's dashboard until *they* fix the root cause.