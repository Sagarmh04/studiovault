Enterprise Vendor Portal (Freelancer Access)

StudioVault Vendor Portal enables secure collaboration with external freelancers
without exposing sensitive business or financial data.

Vendors are not employees. Their access is scoped, temporary, and audited.

---

## 1. Context & Goal

Goal:
Integrate external staff (second shooters, makeup artists, assistants)
without compromising business confidentiality.

Core Rule:
A Vendor may see operational details, but never:

- Client contract value
- Agency profit margins
- Other vendors’ pay rates

---

## 2. Limited Vendor Login Dashboard

Access:
Vendors log in via partners.studiovault.in

Visible Scope:
- My Assignments (only projects where Vendor_ID is tagged)
- Call Sheets (location, schedule, team)
- Shoot Brief (Mood Board / Shot List, optional)

Hard Restrictions:
- No CRM access
- No client phone/email unless explicitly granted
- No finance visibility

---

## 3. Remote Ingest Workflow (Write-Only Upload)

Problem:
Freelancers often deliver SD cards physically, delaying editing workflows.

Feature: Remote Ingest
1. Vendor opens Assigned Project
2. Clicks "Upload Footage"
3. System generates a Write-Only Pre-signed URL
4. Vendor uploads files directly into:

   Project_Bucket/Ingest/Vendor_Name/

Security Model:
- Vendor can upload
- Vendor cannot download, delete, or browse existing files
- WORM behavior (Write Once Read Many)

---

## 4. Vendor Invoice Submission (Accounts Payable)

StudioVault does not operate an internal wallet or stored-value payout system.

Workflow:
1. Job Complete → Vendor prompted: "Submit Invoice for Project X"
2. Vendor enters amount + uploads PDF invoice
3. Manager receives approval notification
4. Manager reviews work → Approves or Rejects

If Approved:
- Invoice is recorded into the Agency’s Accounts Payable ledger
- Payment occurs externally via the Agency’s normal banking process
  (StudioVault does not intermediate vendor money flows)

StudioVault acts as workflow + recordkeeping infrastructure, not a funds holder.

---

## 5. Compliance & Audit

All vendor actions are logged:

- Assignment creation/removal
- Upload timestamps
- Invoice submission events
- Approval decisions

Vendor access is automatically revoked after project closure unless extended.
