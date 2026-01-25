# Data Portability & Compliance

## 1. Context
* **Requirement:** GDPR and Indian DPDP Act compliance. Users must be able to leave the platform with their data.
* **Philosophy:** "Easy Exit." We retain users by quality, not by holding data hostage.

## 2. The "Takeout" Module
* **Location:** Settings -> Data Management -> "Export My Data".
* **Formats:**
    * **Client List:** `.CSV` (Standard format for importing into other CRMs).
    * **Financials:** `.PDF` (Invoices) and `.CSV` (Ledger).
    * **Project Metadata:** `.JSON` (Machine-readable structure).
* **Security:** Export link is sent to the Owner's email (2FA required) to prevent staff from stealing the client list.

## 3. Data Deletion (The "Right to be Forgotten")
* **User Action:** "Delete Account".
* **System Process:**
    * **Grace Period:** Account enters "Suspended" state for 30 days (Recoverable).
    * **Hard Delete:** After Day 30, all PII (Personally Identifiable Information) is scrubbed from the DB.
    * **Retention:** Financial transaction logs are kept for 7 years (anonymized) for Tax Audits, as required by law.