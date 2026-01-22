# Global Audit & Security Log

## 1. Retention Policy
* **Standard Tier (Free):** **90 Days Rolling.**
    * Logs older than 90 days are auto-purged.
* **Extended Tier (Paid Add-on):**
    * Option to extend retention to 1 Year, 3 Years, or "Forever" for compliance.
    * Rate: TBD (Future Pricing Model).

## 2. Visibility Scopes
* **HQ View (Global):**
    * Sees **ALL** events from **ALL** branches + Organization settings changes.
    * Filterable by: Branch, User, Severity, Date.
* **Branch View (Local):**
    * Location: "Agency Mode" Branch Dashboard -> Audit Tab.
    * Scope: Strictly filtered to events linked to `Current_Branch_ID`.
    * *Restriction:* Manager cannot see what happens in other branches.

## 3. Event Triggers (What gets logged?)
We track **High-Risk Actions** only (to reduce noise).
* **Financial:**
    * Invoice Deletion / Voiding.
    * Refunds > ₹0.
    * Price Overrides > 10%.
* **Operational:**
    * Project Deletion.
    * Asset Status Change (Active -> Lost/Stolen).
* **Security:**
    * User Role Changes.
    * Branch Settings Edits.
    * Failed Login Attempts (Spike detection).

## 4. Role Constraints
* **Branch Manager:**
    * Can VIEW their branch logs.
    * **Cannot** Edit/Delete logs (Immutable).
    * **Cannot** Create/Switch Branches (This is an Org-Owner privilege).