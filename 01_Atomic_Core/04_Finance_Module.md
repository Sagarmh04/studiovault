# Finance Module

## 1. Wallet System (Nodal Model)
* **Regulatory Compliance:** We use a Nodal Account provider (RazorpayX/Cashfree). We do *not* hold funds.
* **Flow:**
    * Customer Payment -> Nodal Account.
    * **Split:** Platform Fee (to Us) / Net Amount (to User's Virtual Wallet).
* **Promotional Credits:** "Cashback" added to Wallet is flagged `Non-Withdrawable`. Can only be used for Subscription/Add-ons.

## 2. Withdrawal Logic (The "Payout" Rules)
* **Mechanism:** User triggers payout -> Nodal sends to their Bank Account.
* **Fees & Limits:**
    * **Tier 1 (First 2 Withdrawals/Month):** **FREE**. (StudioVault absorbs the banking cost).
    * **Tier 2 (3rd Withdrawal onwards):** Charged at cost (e.g., ₹10 per txn) deducted from the payout amount.

## 3. Tax Logic
* **Responsibility:** The Photographer/Studio defines the Tax %.
* **Merch vs Service:**
    * System supports distinct tax rates for Goods (e.g., 12%) and Services (e.g., 18%).
    * Invoices clearly separate these line items.

## 4. Platform Fees
* **Free Plan:** 2-3% "Processing Fee" added to the Customer's Total Bill (Pass-through).
* **Paid Plan:** Zero/Low fee options.