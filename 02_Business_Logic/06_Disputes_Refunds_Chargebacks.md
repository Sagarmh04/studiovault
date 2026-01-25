Disputes, Refunds & Chargebacks (The Money Reality Layer)

Payments are not final states.
They are reversible, disputable, and sometimes fraudulent.

StudioVault must protect studios from abuse while remaining fair to clients.

This document defines the Phase 1 financial dispute state machine.

---

## 1. Core Principles

- Refunds are high-risk actions
- Chargebacks are existential threats to trust + revenue
- Delivery completion changes refund eligibility
- Governance thresholds prevent insider misuse

StudioVault does not hold funds.
All refunds occur via payment gateway reversal flows.

---

## 2. Refund Authority Model (Phase 1)

Default Rule:
Refund initiation is an Owner-controlled action.

### Roles

Owner:
- Full refund authority

Manager:
- May request or execute refunds only below configured thresholds

Clerk/Staff:
- No refund privileges

---

## 3. Configurable Refund Thresholds (Governance Controls)

Organizations may define limits such as:

- Refund Cap:
  IF Refund Amount > ₹15,000 → Manager blocked → Owner approval required

- Discount Cap:
  IF Discount > 15% → Approval required

These rules are enforced centrally and logged immutably.

---

## 4. Refund Eligibility Rules (Delivery Lock)

Refunds are blocked by default once final delivery has occurred.

Delivery Event Definition:
- Client portal marked Delivered
- Final gallery download access enabled

Policy:
- Post-delivery refunds require HQ override approval
- This prevents "download → refund → vanish" fraud

Owner may optionally enable partial refund policies.

---

## 5. Gateway Fee Handling (Non-Refundable Costs)

Payment gateway fees are typically non-recoverable.

Default Policy:
- Client refund is processed net of gateway fees

Example:
- Client paid ₹10,000
- Gateway fee ₹250 (non-refundable)
- Refund executed = ₹9,750

Owner Override Option:
Branch Owners may choose to absorb fees as a goodwill policy.

StudioVault exposes this as a configurable setting, not a hard rule.

---

## 6. Chargeback State Machine

Chargebacks are disputes raised externally through the client’s bank/card provider.

### States

1. PAID
- Transaction completed successfully

2. DISPUTED
- Chargeback opened by client bank
- Studio notified immediately

3. UNDER_REVIEW
- Evidence collection window
- Studio uploads proof (contract, delivery logs)

4. RESOLVED (WON)
- Funds remain with studio
- Transaction returns to PAID

5. RESOLVED (LOST)
- Funds reversed to client
- Chargeback fee applied

---

## 7. Delivery Portal Enforcement During Disputes

Default Policy:
- Delivery portal is NOT frozen when a dispute is opened

Freeze Rule:
- Portal freeze occurs only if dispute is LOST

Rationale:
- Prevents harming legitimate clients during investigation
- Still protects studios after confirmed reversal

Owner Override:
HQ may manually freeze access during active disputes if fraud is suspected.

---

## 8. Audit & Compliance Logging

All refund/dispute events are logged:

- Refund requests
- Approval decisions
- Gateway reversal confirmations
- Chargeback state transitions

Logs are immutable and visible only to authorized HQ roles.

---

## 9. Future Enhancements (Phase 2)

- Automated fraud scoring (repeat refund clients)
- Partial refund workflows
- Escrow-like milestone payments for enterprise
- Insurance-style dispute protection tiers

---

## 10. Trust Doctrine

Refunds are empathy.
Chargebacks are war.
Governance is survival.

StudioVault enforces fairness without allowing abuse.
