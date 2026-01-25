Agency Governance & Approval Engine

Goal:
Replace blind trust with systematic control in multi-branch agencies.

StudioVault enforces thresholds for high-risk financial actions.

---

## 1. Context

Problem:
A branch manager could issue large refunds or extreme discounts without oversight.

Solution:
Threshold-based HQ approval.

Actions below limits are instant.
Actions above limits require Owner sign-off.

---

## 2. Threshold Logic (Default Rules)

Configured in Global Settings.

Recommended Triggers:
- Discount Cap: >15% requires approval
- Refund Cap: >₹5,000 requires approval
- Project Deletion: Signed projects require approval
- Invoice Voiding: Paid invoices require approval

---

## 3. Refund & Payment Compliance (No Wallet)

StudioVault does not issue wallet credits or hold refundable balances.

Refunds occur via the payment gateway:

- Refund is initiated against the original transaction
- Funds return directly to the client through provider reversal flows

Governance applies to *authorization*, not custody of funds.

---

## 4. Approval Workflow

Step 1: Request (Branch)
- Manager attempts refund of ₹20,000
- System blocks action → Request Approval modal

Step 2: Decision (HQ)
- Owner receives notification
- Approves or rejects with comment

Step 3: Execution (System)
- If approved: Refund request sent to payment provider
- If rejected: Transaction remains unchanged

All events logged in Global Audit.

---

## 5. Emergency Overrides

Organization Owner is exempt from thresholds.

Audit Trail:
Every approval/rejection is immutable and timestamped.

---

## 6. Automated Enforcement (Smart Watermark Rule)

Rule:
If Invoice Balance > 0 → Watermark forced

Managers cannot disable watermarking on unpaid projects unless HQ approves.
