# Enterprise Vendor Portal (Freelancer Access)

## 1. Context & Goal
* **Goal:** Securely integrate external staff (Second Shooters, Makeup Artists) without exposing sensitive business data.
* **The "Privacy Wall":** A Vendor must see *where* to go and *what* to shoot, but **NEVER** see the Client's Contract Value or the Agency's Profit.

## 2. The "Limited" Login Dashboard
* **Access:** Vendors log in via `partners.studiovault.in`.
* **View Scope:**
    * **My Assignments:** List of active jobs where `Vendor_ID` is tagged.
    * **Call Sheets:** Read-only view of Location, Schedule, and Team.
    * **Shoot Brief:** "Mood Board" and "Shot List" visibility (Optional).
* **Restrictions:**
    * **No CRM:** Cannot see Client Phone/Email (unless "Lead Shooter" permission is granted).
    * **No Finance:** Cannot see the Project Invoice or other vendors' pay rates.

## 3. The "Ingest" Workflow (Raw Uploads)
* **Problem:** Freelancers usually hand over SD cards physically, delaying the edit.
* **Feature:** **Remote Ingest.**
    * Vendor opens Assigned Project -> Clicks "Upload Footage".
    * System generates a **Write-Only** Pre-signed URL.
    * Vendor uploads Raw files directly to `Project_Bucket/Ingest/Vendor_Name/`.
* **Security:** Vendor can *upload* files but cannot *download* or *delete* files once uploaded (WORM - Write Once Read Many).

## 4. Financials (Invoice Submission)
* **The Cycle:**
    1.  **Job Complete:** System prompts Vendor: "Submit Invoice for Project X".
    2.  **Upload:** Vendor enters Amount + Uploads PDF.
    3.  **Approval:** Manager receives notification.
        * *Action:* Checks footage -> Clicks "Approve".
    4.  **Payout:** Amount is added to the "Accounts Payable" list in the Finance Module.