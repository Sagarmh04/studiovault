Security Threat Model & Access Hardening (The Paranoia Layer)

StudioVault manages client identities, booking revenue, and irreplaceable media.
Security is not a feature — it is a condition of existence.

This document defines what we defend against in Phase 1.

---

## 1. Core Security Philosophy

StudioVault assumes:

- Mistakes happen
- Staff misuse is the dominant real-world threat
- Financial flows attract fraud
- Least privilege is mandatory

Security must be practical, not theatrical.

---

## 2. Authentication & Identity Controls

### 2FA Policy (Phase 1)

Two-Factor Authentication is supported but optional for all users.

- Owners are strongly encouraged to enable 2FA
- Enterprise tiers may enforce mandatory 2FA later

---

## 3. Session Security

Default Session Policy:
- 30-day rolling sessions

Rule:
- If a user logs in again within 30 days, the session timer may refresh.

Remember Me Option:
- Extended sessions are supported for usability
- Users must retain the ability to revoke sessions remotely

Indefinite sessions are not recommended for high-risk roles.

---

## 4. Re-Authentication for High-Risk Actions

Sensitive actions require password confirmation (step-up auth):

- Project deletion
- Refund initiation
- Client database export
- Role or permission changes
- Branch-level billing enforcement overrides

This prevents damage from unattended logged-in devices.

---

## 5. Encryption & Data Protection

StudioVault enforces:

- Encryption in transit via HTTPS/TLS for all traffic
- Provider-managed encryption at rest for stored data
  (Cloudflare R2/D1 and hosting infrastructure)

Raw credentials and payment details are never stored directly by StudioVault.

---

## 6. Primary Threat Priorities (Realistic)

Phase 1 threat model focuses on:

### A) Insider Misuse (Staff Risk)
- Unauthorized client list exports
- Abuse of discounts/refunds
- Cross-branch data leakage

Controls:
- RBAC enforcement
- Scoped search boundaries
- Audit logging of high-risk actions

### B) Payment Fraud & Dispute Abuse
- Fake refund attempts
- Chargebacks after delivery
- Payment manipulation via staff privilege misuse

Controls:
- Approval thresholds for refunds
- Immutable financial audit trails
- Gateway-based reversal handling

---

## 7. Vendor & Freelancer Security Boundary

Default Policy:
- Vendor access expires after project completion unless explicitly extended

Vendors must never access:
- Client contract values
- Agency profits
- Other vendor rates
- Full CRM exports

Uploads are write-only (WORM model).

---

## 8. Audit & Forensics

Security-sensitive events are always logged:

- Role changes
- Refund approvals
- Export actions
- Failed login spikes
- Project deletions

Logs are immutable and visibility-scoped:

- Branch managers see only branch events
- Owners/HQ see organization-wide events

---

## 9. Future Hardening (Phase 2+)

- Mandatory 2FA for Owners
- Short-lived privileged sessions
- Device-based trust controls
- Multi-region resilience for enterprise
- Automated anomaly detection (fraud signals)

---

## 10. Trust Doctrine

Studios trust systems that prevent silent disasters.

Security is not paranoia.
Security is professionalism.
