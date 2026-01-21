# Resource Module: Inventory & Availability

## 1. Asset Classes
* **Fixed Assets:** Cameras, Lenses, Lights, Drones. (Tracked by Serial Number).
* **Spaces:** Physical Rooms (e.g., "Green Screen Floor").
* **Human:** Photographers, Editors, Makeup Artists.

## 2. The "Lock" Mechanism
* **Goal:** Prevent double-booking.
* **Logic:** * Every Booking consumes specific resources for a specific time slot.
    * *Conflict Check:* `IF (Asset_A is Reserved) AND (New_Booking requires Asset_A) -> REJECT`.

## 3. Maintenance & Status
* **States:** Available, Booked, Maintenance, Lost/Stolen.
* **Logs:** Custody chain tracking. "Who had the Sony A7iii last?"