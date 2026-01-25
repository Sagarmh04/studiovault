Communication Hub

StudioVault communication is scoped, contextual, and compliance-aware.
Messaging is designed to support bookings and delivery workflows without
becoming a spam engine.

---

## 1. The Scoped Chat System

Chat is not global; it is Context-Aware.

### Context A: Lead / Inquiry (Pre-Booking)
- Scope: Transient, linked to Lead_ID
- Rules: Optional regex filtering (commission/privacy mode)

### Context B: Project (Post-Booking)
- Scope: Permanent, linked to Project_ID
- Header: Messages display context ("Regarding: Wedding Package A")
- Capabilities: File sharing enabled

This prevents staff from mixing unrelated client conversations.

---

## 2. Notification Engine

Notifications are event-driven and tier-governed.

### Trigger Types

**Internal (Staff):**
- New Inquiry
- Payment Failed
- Storage 90% Full

**External (Client):**
- Booking Confirmed
- Invoice Due
- Photos Ready
- Contract Signed

---

## 3. Routing & Priority Rules

### High Priority Channels (Transactional)
Used only for revenue-critical workflows:
- Booking confirmations
- Payment reminders
- Delivery alerts

Delivered via:
- WhatsApp / SMS (depending on client availability)

### Low Priority Channels
- Email summaries
- Non-urgent updates

Marketing is handled only through the Marketing Engine module
(opt-in enforced).

---

## 4. Quotas & Billing (No Wallet)

StudioVault does not deduct notifications from an internal wallet.

### Included Quota
- 60 notifications/month per branch included by default

### Overage Handling
After quota exhaustion:

- WhatsApp: ₹0.25 per message
- SMS: ₹0.45 per message

All overages are added automatically to the month-end invoice.

---

## 5. Overdue Enforcement

If an account becomes overdue beyond the billing grace period:

- High-priority notifications may be paused to prevent unpaid usage
- Email remains the fallback channel for critical system alerts

Delivery portal enforcement remains the primary escalation mechanism.

---

## 6. Privacy Bridge (Marketplace Mode)

For marketplace-driven leads (e.g., RealCandid):

- Phone numbers remain masked
- StudioVault relays messages between Client ↔ Photographer
- Direct contact details are revealed only after Booking Confirmation

This protects both client privacy and platform integrity.
