Global Finance & Expense Management

Finance settings operate at the Organization layer.

StudioVault billing is invoice-based, not wallet-based.

---

## 1. Expense Tab Strategy

Location:
Organization Settings → Finance

Philosophy:
Manual entry only (expenses are too complex for automation)

User Action:
Owner/Finance Manager inputs fixed costs per branch.

---

## 2. Expense Input Module

Granularity:
Per Branch

Fields:
- Fixed Monthly Cost (Rent, Utilities)
- Staff Salaries (Lump sum or itemized)
- Marketing Budget (Manual)

Persistence:
System applies these monthly until changed.

---

## 3. Profit Calculation Formula

Location:
Global Pulse → Profitability Widget

Formula:

Estimated Profit =
(Net Sales) - (Fixed Monthly Expenses + Vendor Costs)

Disclaimer:
Shown as "Operational Estimate (EBITDA)", not taxable net income.

---

## 4. Centralized Billing (Invoice Model)

StudioVault subscription charges are billed monthly.

Organization Invoice Includes:
- Branch subscriptions
- Org HQ governance fee (if enabled)
- Storage overages
- Messaging overages
- Optional enterprise add-ons

Payment Handling:
- Invoices are paid via standard payment methods (Card/UPI/NetBanking)
- No stored wallet balance exists

Overdue Enforcement:
- Grace period: 7 days
- Post-grace: Delivery portals frozen + uploads blocked
