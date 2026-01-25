# Booking Engine & Project Packages (Event Workflow System)

## 1. Booking Domain Definition

The Booking Engine exists for scheduled, contractual projects:

- Weddings
- Commercial shoots
- Multi-day events
- Deliverable-based client work

Booking creates Projects.

Projects include:

- lifecycle stages
- contracts
- delivery portals
- payment enforcement
- calendar locking

Booking is NOT for passport-photo walk-ins.

Walk-ins belong exclusively to the POS module.

---

## 2. Package Architecture (Project Packages Only)

Packages here represent scheduled services.

Types:

- **Project Package (Time-Based)**
  Example: "Wedding – 8 Hours"

Attributes:

- Name
- Base Price
- Tax metadata
- Inclusions (Drone, Album)
- Exclusions (Travel, Extra hours)
- Resource hooks:
  "Requires 1 Lead Photographer + Sony A7iii"

Fast POS packages do NOT belong here.

---

## 3. Online Booking Flow (Inquiry → Confirmation)

### Step 1: Inquiry
Client requests a quote or package.

Status: `Inquiry`

Calendar Behavior:

- Soft hold only (no hard lock)

### Step 2: Negotiation
Studio discusses pricing/date via scoped chat.

### Step 3: Agreement & Activation
Project becomes ACTIVE only when:

- Photographer explicitly accepts
OR
- Client pays required advance

Final concurrency check occurs before payment capture.

Payment Success →

Status: `Booked`

Calendar: Hard Lock applied

---

## 4. Manual Project Booking (Staff-Created Event Booking)

Some studios book events manually through staff dashboards.

This is NOT POS Walk-In.

Workflow:

- Manager enters Client + Event Date/Time
- Project is immediately activated
- Calendar is hard-locked
- Counts toward Active Project limits (Free tier)

Purpose:

- Handles offline business operations for large events
- Supports bookings that happen without online checkout

---

## 5. Explicit Boundary Rule

StudioVault enforces a strict separation:

- Booking Engine → Scheduled Projects (Events)
- POS Module → Instant Walk-In Sales (Passport, Counter)

Walk-In transactions never enter the Booking lifecycle.
Projects never behave like POS receipts.


# One Warning (Very Important)

You must ensure database separation too:

- `quick_orders` (POS)
    
- `projects` (Bookings)
    

Never merge them later or reporting becomes impossible.

POS = receipts  
Booking = lifecycle + delivery

