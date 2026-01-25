Finance Module (Invoice-Based, No Wallet)

StudioVault operates as a SaaS platform, not a stored-value wallet provider.
We do not hold user funds. All money flows are routed directly through regulated
payment infrastructure.

---

## 1. Payment Flow (Direct Settlement Model)

**Regulatory Principle:**
StudioVault does *not* store or hold customer money in an internal wallet.

**Provider Layer:**
Payments are processed via Razorpay / Cashfree using compliant routing
mechanisms (Nodal / Split Settlement where required).

**Flow:**
1. Client pays ₹10,000 via StudioVault booking link.
2. Payment gateway processes transaction.
3. Settlement is routed directly:

   - Payment Gateway Fee (~2.5%) deducted by provider
   - StudioVault Platform Fee (tier-based) deducted automatically
   - Remaining amount settles directly to the Photographer/Studio bank account

StudioVault never maintains a withdrawable balance for the user.

---

## 2. Platform Fee Model (Per Booking)

StudioVault monetizes bookings via a transparent platform fee.

**Free Plan:**
- Total Processing Fee: 5%
  - ~2.5% Gateway Fee
  - ~2.5% StudioVault Platform Fee

**Pro Plan:**
- Total Processing Fee: 3.5%
  - ~2.5% Gateway Fee
  - ~1.0% StudioVault Platform Fee

**Enterprise / Agency Mode:**
- StudioVault Platform Fee: 0%
- Only gateway fees apply

Fees are shown as a single combined processing charge to the client.

---

## 3. Month-End Billing (No Wallet)

Since StudioVault does not operate a wallet system:

- Storage overages
- Notification overages (WhatsApp/SMS)
- Organization HQ fees
- Subscription charges

…are aggregated into a single **month-end invoice**.

**Billing Rules:**
- Invoice generated at month-end
- 7-day grace period after due date
- After grace period:
  - Uploads blocked
  - Delivery portal frozen

**Non-payment Enforcement:**
- Day 45: Final warning + One-click Export ZIP
- Day 60: Storage eligible for deletion if unpaid

---

## 4. Tax & Invoice Logic

**Responsibility:**
The Photographer/Studio defines applicable tax rates.

**Support:**
- Goods tax (e.g., 12%)
- Service tax (e.g., 18%)

Invoices clearly separate:

- Service line items (shoot packages)
- Merchandise line items (albums, frames)
- Taxes applied per category

StudioVault provides invoices as infrastructure,
but tax compliance remains the studio’s responsibility.

---

## 5. Promotional Credits (Future Scope)

StudioVault does not currently issue stored-value cashback credits.

Future promotional models (if introduced) will be applied only as:

- Invoice discounts
- Subscription coupons

Never as withdrawable balances.

---

## 6. Key Compliance Statement

StudioVault is an invoicing + workflow SaaS platform.

- No internal wallet
- No stored user balances
- No user-triggered withdrawals
- Direct regulated settlement to studio accounts

This architecture avoids RBI stored-value classification risk.

## Tax Location Logic (Global-Compatible)

StudioVault supports tax calculation based on jurisdiction rules.

### Phase 1 Principle
Tax bucket selection depends on:

- Branch Location (Seller jurisdiction)
- Client Location (Supply jurisdiction)

### India GST Example (Default Helper)
- Same State → CGST + SGST
- Different State → IGST

### Global Generic Rule
If jurisdiction data is missing:

- System assumes same-jurisdiction by default
- Invoice UI displays: "Tax Location Not Specified"
- Owner may override manually

### Future Expansion
Tax engines will remain modular so other countries (VAT, Sales Tax)
can be added without redesigning invoices.
