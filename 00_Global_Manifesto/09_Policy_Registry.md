Policy Registry (The Single Source of Enforcement Truth)

StudioVault rules must not live in scattered modules.
Every enforcement action must map cleanly to:

- Product behavior
- Billing outcomes
- Legal Terms disclosure

This registry is the canonical truth table for all hard policies.

---

## 1. Billing Enforcement Policies

### Invoice Grace Period
- Rule: Invoices are due monthly
- Grace Period: 7 days after due date

Enforcement After Grace:
- Uploads blocked
- Delivery portal frozen

Terms Reference:
- Billing & Suspension Clause

---

### Overdue Data Safeguard Window
- Day 45: Final warning issued
- Day 45: One-click Export ZIP provided
- Day 60: Storage eligible for deletion if unpaid

Terms Reference:
- Data Retention + Non-Payment Clause

---

## 2. Data Deletion & Recovery Policies

### Project Trash Window
- Deleted projects enter Trash for 30 days
- Recoverable by Owner/Admin during this window
- Hard delete after expiry

Terms Reference:
- Deletion & Recovery Clause

---

### Account Deletion
- Account enters Suspended state for 30 days
- PII scrubbed after Day 30
- Financial logs retained 7 years (anonymized)

Terms Reference:
- Right to be Forgotten Clause

---

## 3. Storage & Upload Policies

### Free Tier RAW Restriction
- Free tier cannot upload RAW formats directly
- Must use Smart Select proxy bridge

Terms Reference:
- Plan Limitations Clause

---

### Storage Overage Billing
- Rate: ₹4.5/GB/month (India baseline)
- Added to month-end invoice (no wallet)

Terms Reference:
- Usage Charges Clause

---

## 4. Messaging & Notification Policies

### Included Quota
- 60 notifications/month per branch

Overage Rates:
- WhatsApp: ₹0.25/msg
- SMS: ₹0.45/msg

Billing:
- Added to monthly invoice automatically

Terms Reference:
- Messaging Charges Clause

---

## 5. Refund & Dispute Governance Policies

### Refund Authority
- Owner has full refund authority
- Managers limited by approval thresholds

Default Threshold Example:
- Refund > ₹15,000 requires Owner approval

Terms Reference:
- Refund Authorization Clause

---

### Delivery Refund Lock
- Refunds blocked by default after final delivery
- Override requires HQ approval

Terms Reference:
- Delivery Completion Clause

---

### Gateway Fee Refund Rule
Default:
- Refunds processed net of gateway fees

Owner Override:
- Studio may absorb fees optionally

Terms Reference:
- Payment Processing Clause

---

### Chargeback Handling
States:
- Paid → Disputed → Under Review → Resolved (Won/Lost)

Portal Freeze Policy:
- Freeze only if dispute is lost

Terms Reference:
- Chargeback & Dispute Clause

---

## 6. Security Enforcement Policies

### Step-Up Authentication Required
Password confirmation required for:

- Refund initiation
- Client export
- Project deletion
- Role changes

Terms Reference:
- Account Security Clause

---

### Vendor Access Expiry
Default:
- Vendor access expires after project completion

Terms Reference:
- Third-Party Access Clause

---

## 7. Logging & Audit Policies

### Audit Log Retention
- Free tier: 90 days
- Paid extensions: up to 1 year+

Operational Log Retention:
- 30 days rolling

Terms Reference:
- Audit & Compliance Clause

---

## 8. Governance Rule

If product behavior changes,
Policy Registry must be updated before release.

Policy drift is a compliance failure.

---

## 9. Trust Doctrine

Rules must be explicit.
Enforcement must be predictable.
Surprises destroy trust.
