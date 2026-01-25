Integration Architecture & Guardrails

This document defines the technical safeguards for StudioVault integrations:
Payments, Notifications, and Storage enforcement.

StudioVault operates without an internal wallet system.

---

## 1. Notification Engine (Meta Tech Provider Model)

Objective:
Allow users to bring their own WhatsApp number without touching API keys.

Architecture: Embedded Signup (OAuth)
- Uses facebook-login flow with whatsapp_business_management scope

Routing:
- Route A (Transactional): Sent via StudioVault_Main_Number (platform-paid)
- Route B (Marketing): Sent via User_Connected_WABA_ID (Meta bills user directly)

---

## 2. Payment Gateway (Regulatory Compliance Layer)

Provider:
Razorpay Route / Cashfree Split Settlement

Key Principle:
StudioVault does not hold user funds or maintain stored balances.

Payment Flow Example:
1. Customer pays ₹10,000
2. Deductions occur automatically:

   - Gateway Fee (~2.5%) retained by provider
   - StudioVault Platform Fee (tier-based)
   - Optional Compliance Deductions (e.g., TDS if applicable)

3. Remaining amount settles directly to the Photographer/Studio bank account

StudioVault never routes money into an internal wallet.

---

## 3. Refund Strategy (Direct Reversal Model)

Refunds are handled via the payment provider:

- Refund initiated from original transaction
- Settlement reversed directly back to the customer
- No wallet crediting occurs

High-risk refunds may require HQ approval (Governance Controls module).

---

## 4. Secure Storage (Event-Driven Quota Enforcement)

Upload Flow:
1. Client requests pre-signed URL
2. Backend validates session + enforces max Content-Length
3. Client uploads directly to R2

Quota Truth Source:
- ObjectCreated webhook triggers backend update
- Exact bytes written into Storage_Used table

Billing Link:
- Storage overages are added to month-end invoice (no wallet deduction)

Future Scope:
- Virus scanning via Lambda + ClamAV
