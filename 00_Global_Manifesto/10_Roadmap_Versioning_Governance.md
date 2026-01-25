Roadmap Governance & Versioning (The Anti-Chaos Protocol)

StudioVault is a long-lived operating system for studios.

Systems that handle bookings, payments, and legal contracts must evolve
without breaking trust.

This document defines how StudioVault changes over time.

---

## 1. Core Principle

Every change has a blast radius.

StudioVault must never:

- Break existing contracts
- Mutate active packages silently
- Surprise studios with enforcement shifts
- Drift product behavior away from documented policy

Versioning is governance.

---

## 2. Version Domains

StudioVault maintains explicit versioning across:

1. Package Templates
- Master templates have version numbers (v1, v2…)

2. Contract Documents
- Signed contracts are immutable
- Changes create amendments (Contract_v2)

3. Pricing & Policy Rules
- Policy Registry governs enforcement truth

4. Data Schema Changes
- Migrations must preserve backward compatibility

---

## 3. Upgrade Rules (No Silent Overwrites)

### Packages
HQ updates do not auto-overwrite branch copies.

Instead:
- Branch sees "Update Available"
- Manager reviews diff
- Manager accepts or ignores

This prevents breaking active client expectations.

---

## 4. Policy Change Discipline

If enforcement changes (billing grace, deletion windows, refund locks):

Required Steps:
1. Update Policy Registry first
2. Update Terms mapping
3. Notify users before enforcement date
4. Apply only prospectively where possible

Policy drift is a compliance failure.

---

## 5. Feature Rollout Governance

New enterprise modules are rolled out through:

- Feature flags
- Tier gating
- Controlled pilot branches

No global rollout without stabilization.

---

## 6. Backward Compatibility Doctrine

StudioVault guarantees:

- Old projects remain accessible under the rules they were created with
- Signed contracts remain enforceable forever
- Delivery links remain stable unless explicitly expired

---

## 7. Roadmap Classification System

All scope is tagged:

- ATOMIC CORE (Must ship Phase 1)
- AGENCY PHASE (Multi-branch governance)
- ENTERPRISE MOATS (Marketing, Video Ops, Vendor Portal)
- ICEBOX (Deferred, optional future)

This prevents roadmap inflation.

---

## 8. Trust Doctrine

A studio’s business is not a beta test.

StudioVault evolves with:

- versioning
- notification
- consent
- restraint
