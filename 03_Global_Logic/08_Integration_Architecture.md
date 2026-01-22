# Integration Architecture & Guardrails

## 1. Notification Engine (Meta Tech Provider Model)
* **Objective:** Allow users to bring their own WhatsApp number without touching code.
* **Architecture:** **Embedded Signup (Oauth).**
    * We do NOT ask for API Keys.
    * We use the `facebook-login` flow with `whatsapp_business_management` scope.
    * **Route A (Transactional):** Sent via `StudioVault_Main_Number` (Platform pays).
    * **Route B (Marketing):** Sent via `User_Connected_WABA_ID` (User pays Meta directly via credit card attached to their WABA).

## 2. Payment Gateway (The Regulatory Compliance Layer)
* **Provider:** Razorpay Route / Cashfree Splits.
* **The "India Stack" Split Logic:**
    1.  **Inflow:** Customer pays ₹10,000.
    2.  **Deduction 1 (Platform Fee):** ₹300 (3%) -> StudioVault Ops Account.
    3.  **Deduction 2 (TDS Compliance):** ₹100 (1% of Gross) -> StudioVault Tax Account (To be filed against Vendor's PAN).
    4.  **Settlement:** ₹9,600 -> Vendor's Linked Account (Frozen until KYC).
* **Refund Strategy:**
    * Enable "Reversals" on the Linked Account.
    * If refund is triggered, System initiates `Reverse Transfer` from Vendor -> Master -> Customer.

## 3. Secure Storage (The Event-Driven Quota)
* **Upload Flow:**
    1.  **Auth:** Client requests Pre-signed URL. Backend validates Session.
    2.  **Constraint:** Backend enforces `Content-Length` max limit in the signature.
    3.  **Direct Upload:** Client uploads to R2.
* **Sync Flow (The Truth Source):**
    * **Trigger:** R2/S3 `ObjectCreated` Webhook -> Lambda.
    * **Action:** Lambda updates `User_Storage_Used` table with exact byte size.
    * **Virus Scan:** (Phase 2) Lambda triggers ClamAV scan. If positive, delete file and flag user.