# POS & Walk-In Sales Module (Instant Counter Transactions)

## 1. Context & Scope

POS Walk-In is NOT a booking system.

It is a counter-sale engine designed for:

- Passport photos
- Stamp prints
- Frames and small merch
- 5-minute studio services

This module is operationally different from event bookings.

* **Target User:** Receptionist / Clerk
* **Platform:** Desktop Application only (Electron)
* **Goal:** Maximum speed, zero scheduling complexity
* **Core Principle:** Walk-ins do NOT create Projects

Walk-In sales never:

- enter Inquiry or Booking lifecycle
- lock the calendar
- count toward Active Project caps
- generate delivery portals
- require advance payments

They are instant service transactions.

---

## 2. Data Principle: Append-Only Sales Ledger

POS transactions are chronological and immutable.

* Corrections are new entries, not overwrites
* Deletions are logged as "Voided Transactions"

Reason:

- Prevents sync conflicts
- Preserves financial auditability

---

## 3. Interface Logic (Counter Speed UX)

* **Selector Toggle:**
  - If Merch exists → show toggle: `Merch | Photo Services`
  - Default → `Photo Services`

* **Fast Packages (Predefined Pricing):**
  - Prices are fixed, not calculated dynamically
  - Example:
    - "16 Passport Photos" = ₹200
    - "32 Passport Photos" = ₹350

No quote negotiation exists in POS.

---

## 4. Print-to-Bill Workflow

Walk-In services often require instant printing.

Workflow:

1. Clerk selects package ("16 Passport Photos")
2. User selects layout:
   - 4×4 Grid
   - 8×2 Strip
   - 16×1 Strip
3. App opens OS Print Dialog
4. Verification Loop:
   - "Did printing succeed?"

Results:

- Yes → Transaction billed + receipt generated
- No → Transaction cancelled (no revenue recorded)

---

## 5. Custom Billing (Ad-Hoc Sales)

* Clerk can create a manual bill:

- Service Name
- Price Override
- Optional Merch items

Metadata from base packages is preserved for consistency.

---

## 6. Financial Output

POS produces:

- Instant Receipt Invoice
- Cash/Card/UPI payment entry (optional)
- No Project creation

POS is a transaction system, not a workflow system.
