# Identity Module: The Hierarchy

## 1. Structure
* **Tenant (Organization):** The legal entity (e.g., "Pixeldence").
* **Sub-Tenant (Branch):** A physical or logical location (e.g., "Pixeldence Bangalore", "Pixeldence Dubai").
* **User (Member):** An employee/freelancer with a specific Role.

## 2. The Branch Logic
* **Identity:** Each Branch has its own:
    * Address & Contact Info.
    * Tax ID (GST/VAT).
    * Currency Setting (INR vs AED).
    * Invoice Sequence (e.g., `BLR-001` vs `DUB-001`).
* **Subdomain Routing:**
    * URL: `pixeldence.studiovault.in`
    * Visitor Logic:
        * If Org has 1 Branch -> Direct to Portfolio.
        * If Org has >1 Branch -> Show "Select Location" Splash Screen.

## 3. Roles (RBAC)
* **Owner:** Global access. Can delete Org. Access to Wallet.
* **Branch Manager:** Scoped to Branch. Can manage Staff & Inventory. No access to other branches.
* **Staff/Photographer:** Scoped to Assigned Jobs. View-only on Calendar.
* **Freelancer:** Transient access. Can only view specific "Job Cards" they are tagged in.