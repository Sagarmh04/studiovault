Global Command Center (The Organization Dashboard)

The Command Center is the HQ layer of StudioVault.
It provides organization-level visibility across all branches.

StudioVault operates on invoice-based billing, not wallets.

---

## 1. Context & Architecture

Scope: Organization Level (Parent Layer)

Behavior:
- Atomic Mode (1 Branch):
  Displays stats for the single branch, but maintains global structure

- Agency Mode (Multi-Branch):
  Aggregates data across all Branch_IDs linked to this Org_ID

---

## 2. The Currency Engine

Selector:
- Top-right dropdown (e.g., View in USD / INR)

Data Source:
- External FX API (cached in DB for 1 hour)

Frontend Rule:
- Reads strictly from cache (zero latency)

---

## 3. The "Big Numbers" Ticker + Drill-Down

Clicking any metric opens a detailed breakdown.

Core Metrics:
1. Global Gross Revenue
   - Revenue per branch comparison

2. Net Sales
   - Gross minus refunds

3. Active Projects
   - List of active jobs sorted by due date

4. Global Storage Usage
   - Storage distribution by branch

---

## 4. Billing & Forecast Widget (Invoice-Based)

Location:
- Prominent widget (Top Right)

Purpose:
Keep Owners aware of subscription + overage exposure.

Display:
- Next Invoice Date: [Date]
- Estimated Monthly Charges: ₹X,XXX
  (Subscription + Storage Overage + Messaging Overage + Org HQ Fee)
- Account Status:
  - Paid / Due Soon / Overdue

StudioVault does not display wallet balances.
All charges are handled through monthly invoicing.

---

## 5. Exception Feed (Problem Management)

Alert Categories:
- Financial: Overdue invoices, payment failures
- Operational: Double bookings, resource conflicts
- System: Storage limits reached

Lifecycle Logic (HQ Hide):
- HQ may dismiss alerts locally
- Alert remains active on the responsible branch dashboard until resolved

---

## 6. Strategic Role of Command Center

Command Center is not just analytics.
It is the governance interface for multi-branch agencies:

- Visibility
- Billing accountability
- Risk containment
- Expansion management
