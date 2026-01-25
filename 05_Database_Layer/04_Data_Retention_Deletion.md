Data Retention & Deletion Model (The Irreversibility Protocol)

StudioVault stores irreplaceable memories and business-critical records.
Deletion is therefore never casual.

This document defines the canonical retention + deletion lifecycle
for metadata and media.

---

## 1. Core Principles

- No instant destructive deletes
- All deletions pass through a recovery window
- Billing enforcement must include export safeguards
- Legal retention overrides user deletion in specific cases

Deletion is a governance event, not a UI action.

---

## 2. Project Deletion Lifecycle

### Step 1: Soft Delete (Trash)

When a user deletes a project:

- Project status changes to: trashed
- Media remains intact
- Project is hidden from active dashboards

Trash Window:
- 30 days recoverable

Only Owner/Manager may restore during this period.

---

### Step 2: Hard Delete (Irreversible)

After Trash expiry:

- Metadata rows are permanently removed
- Media objects in R2 are deleted
- Audit logs remain (immutable compliance)

Hard delete is executed only via background job, never instantly.

---

## 3. Account Overdue Enforcement Retention

StudioVault is invoice-based.
Non-payment triggers staged enforcement, not surprise deletion.

### Timeline

Day 0:
- Invoice due

Day 7:
- Grace period ends
- Uploads blocked
- Delivery portal frozen

Day 45:
- Final warning notification issued
- One-click Export ZIP enabled

Day 60:
- Storage eligible for deletion if unpaid

Rule:
Deletion is never triggered without export opportunity.

---

## 4. Client Data Retention & Compliance

### Account Deletion (Right to be Forgotten)

User triggers Delete Account:

- Account enters Suspended state for 30 days
- Recoverable within this window

After Day 30:
- Personally Identifiable Information (PII) is scrubbed
- Client names/phones removed or anonymized
- Projects removed except where legally required

---

### Financial Record Retention Exception

Invoices and transaction logs must be retained:

- 7 years (anonymized where required)

Reason:
- Tax audits
- Regulatory compliance
- Dispute evidence

Financial metadata is immutable even if account is deleted.

---

## 5. Media Retention Classes

### Proxy Media (Free Tier)
- Stored until project completion or overdue enforcement deletion

### RAW Originals (Pro Tier)
- Stored as long as subscription is active or overages are paid

### Vendor Ingest Media
- Write-only uploads retained until project resolution
- Subject to project-level deletion lifecycle

---

## 6. User-Configurable Auto-Deletion (Optional Feature)

Studios may enable:

- Auto-delete RAW files after X months post-completion
- Retain only final exports for long-term archive

Purpose:
- Cost control
- Storage hygiene

Auto-delete always respects Trash recovery windows.

---

## 7. Audit Log Immunity

Audit logs are never deleted by user action.

Retention:
- Free tier: 90 days rolling
- Paid: extendable (1 year+)

Reason:
- Fraud prevention
- Compliance traceability

---

## 8. Safety Doctrine

Weddings do not have backups.

StudioVault deletion must always be:

- staged
- reversible (temporarily)
- explicitly warned
- legally compliant
