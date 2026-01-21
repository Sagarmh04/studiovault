# Booking Engine & Packages

## 1. Package Architecture
* **Types:**
    * **Project Package (Time-Based):** "Wedding - 8 Hours". Locks Calendar.
    * **Fast Package (Qty-Based):** "16 Passport Photos". Locks Resources (Hidden 15m slot).
* **Attributes:**
    * Name, Price, Tax Rate.
    * **Inclusions:** Array of strings (e.g., "Drone Shot", "Album").
    * **Exclusions:** Array of strings (e.g., "Travel Cost").
    * **Resource hooks:** "Requires 1 Lead Photographer + 1 Sony A7iii".

## 2. Online Booking Flow (The Quote Loop)
* **Step 1: Inquiry.** Client requests Quote (Specific Package OR Custom).
* **Step 2: Negotiation.**
    * Status: `Inquiry` (Calendar: **Soft Lock** - allows other bookings).
    * Chat: Pricing/Date negotiation via scoped chat.
* **Step 3: Agreement & Payment.**
    * Client accepts final Quote.
    * **Concurrency Check:** System checks Availability *one last time* before processing payment.
    * Payment Success -> Status: `Booked` (Calendar: **Hard Lock**).

## 3. Offline Booking Flow (Walk-in)
* **Manager Action:** Enters "Client Name" + "Date/Time".
* **Logic:**
    * Bypasses Payment Gateway.
    * Counts towards "Active Project Cap" (if Free Tier).
    * Hard Locks the Calendar immediately.