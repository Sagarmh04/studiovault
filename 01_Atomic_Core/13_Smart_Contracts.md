# Smart Contracts Module

## 1. Concept
* **Goal:** Dynamic legal protection that adapts to the specific booking without manual editing.
* **Format:** HTML/PDF Generator with Logic Hooks.

## 2. Logic Engine (Conditional Clauses)
* **Structure:** The Contract Template contains "Logic Blocks".
* **Triggers (Based on Package Attributes):**
    * `IF Package.includes("Drone")` -> Auto-Insert: "Aerial Liability & No-Fly Zone Waiver".
    * `IF Location.type == "Outdoor"` -> Auto-Insert: "Inclement Weather & Rain Delay Policy".
    * `IF Deliverables.includes("Raw")` -> Auto-Insert: "Copyright Transfer & RAW Usage License".

## 3. The Signing Flow
* **Generation:** System compiles the clauses into a single PDF upon Booking.
* **Action:**
    * Sent to Client via Email/Portal.
    * Client clicks "Sign" (Simple E-Signature / Audit Trail).
    * Status updates to `Signed`.
* **Lock:** Once signed, the "Package Items" and "Price" are locked.

## 4. Contract Versioning (The "Change Order" Logic)
* **The Problem:** Clients often change scope (e.g., "Add Drone") *after* signing.
* **The Solution:** We never edit a signed PDF. We version it.
* **Workflow:**
    1.  **Trigger:** Manager modifies a "Locked" project (e.g., Adds ₹5,000 service).
    2.  **System Action:**
        * Flags `Contract_v1` as **Void/Superseded**.
        * Generates `Contract_v2` with updated terms + difference in cost.
    3.  **Client Action:** Client receives "Contract Amendment Request". Must sign `v2` to proceed.
    4.  **Audit:** Both `v1` and `v2` are stored permanently. `v1` is watermarked "VOID".