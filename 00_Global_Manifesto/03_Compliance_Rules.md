# Compliance & Financial Safety

## 1. The Nodal Account Model
* **Money Handling:** StudioVault does *not* hold user funds in a standard bank account.
* **Provider:** RazorpayX / Cashfree Nodal.
* **Flow:** 1.  Customer pays ₹10,000 via StudioVault Link.
    2.  Money hits Nodal Account.
    3.  Split Logic:
        * ₹200 (Platform Fee) -> StudioVault Ops Account.
        * ₹9,800 (User Share) -> User's Wallet (Virtual Ledger).
* **Payout:** User triggers withdrawal -> Nodal pushes to User's Bank Account.

## 2. Privacy & Data Ownership
* **Client Data Scope:** Data belongs to the **Organization (Agency)**, not the individual photographer/freelancer.
* **Sharing:** Branches are siloed by default. Sharing customer profiles between branches requires explicit Admin consent ("Global Client List" toggle).