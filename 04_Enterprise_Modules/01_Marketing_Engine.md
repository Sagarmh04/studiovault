Enterprise Marketing Engine

StudioVault Marketing is an enterprise-grade revenue module, not a spam tool.
It is designed around strict opt-in enforcement and compliant billing.

---

## 1. Context & Goal

Goal:
Turn the passive Client Database into an active Revenue Generator.

Key Principle:
Transactional messaging is platform-governed.
Marketing messaging requires explicit opt-in and higher compliance controls.

Architecture:
Uses Hybrid WhatsApp Routing:

- Transactional Route (System-Owned Number)
- Marketing Route (User-Connected WhatsApp Business Account)

---

## 2. Campaign Manager (Broadcasts)

Function:
Bulk messaging for announcements, offers, and reactivation.

Workflow:
1. Select Audience
   - Example: "All Wedding Clients from 2024"

2. Compose Message
   - Supports variables (Hi {{Name}}...)
   - Supports approved media templates (Image/Video)

3. Cost Estimate
   - System calculates expected cost:
     Audience Size × Meta Per-Message Rate

4. Send or Schedule
   - Campaign is queued for delivery

---

## 3. Billing & Payment Handling (No Wallet)

StudioVault does not operate an internal wallet.

Marketing costs are handled via two compliant routes:

### Route A: User-Connected WABA (Direct Meta Billing)
- User connects their WhatsApp Business Account via Embedded Signup (OAuth)
- Meta charges the user directly via the payment method linked to their WABA
- StudioVault does not intermediate marketing message funds

Best for:
- Large agencies running frequent campaigns

---

### Route B: Platform-Assisted Billing (Invoice Add-On)
- For users without direct Meta billing setup,
  StudioVault may allow limited marketing usage

Charges are:
- Added to the month-end invoice as a Marketing Add-On line item
- Subject to compliance review and usage thresholds

---

## 4. Automation Builder (Drip Sequences)

Function:
Trigger-based sequences that increase Lifetime Value (LTV).

Trigger Examples:
- Project Completed → Send review request after 2 days
- Birthday → Send discount voucher
- Inquiry Stalled → Send portfolio highlight after 3 days

Safety Rule:
If client replies → Sequence stops immediately (handover to human staff)

---

## 5. Audience Segmentation (Smart Filters)

Dynamic Lists update automatically based on client data.

Filters include:
- Spend: VIP Clients (>₹1L lifetime spend)
- Category: Maternity Clients (retarget after 6 months)
- Location: Mumbai clients only

Static Lists:
- Manual CSV imports (e.g., Wedding Expo Leads)

---

## 6. Compliance & Anti-Ban Guardrails

WhatsApp bans are enforced aggressively, so StudioVault applies rails:

- Opt-in required for all marketing broadcasts
- Template approval required for outbound campaigns
- Rate limiting on new accounts
- Immediate suppression if clients report spam

If no connected WABA exists:
- Broadcasts are blocked by default

---

## 7. ROI Tracking

Attribution is handled via Campaign-Linked Inquiries.

Mechanism:
- Every campaign link includes ?utm_source=campaign_id
- If booking originates from that link → revenue is attributed

Report Example:
"Diwali Offer: Cost ₹500 → Revenue ₹50,000 (100× ROI)"

---

## 8. Phase Status

Marketing Engine is an Enterprise Module.
It is optional, gated, and not included in Atomic Phase 1 by default.
