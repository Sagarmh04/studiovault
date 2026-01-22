# Smart Contracts Module

## 1. Concept
* **Goal:** Dynamic legal protection that adapts to the specific booking without manual editing.
* **Format:** HTML/PDF Generator with Logic Hooks.

## 2. Logic Engine (Conditional Clauses)
* **Structure:** The Contract Template contains "Logic Blocks".
* **Triggers (Based on Package Attributes):**
    * `IF Package.includes("Drone")` -> **Auto-Insert:** "Aerial Liability & No-Fly Zone Waiver".
    * `IF Location.type == "Outdoor"` -> **Auto-Insert:** "Inclement Weather & Rain Delay Policy".
    * `IF Deliverables.includes("Raw")` -> **Auto-Insert:** "Copyright Transfer & RAW Usage License".

## 3. The Signing Flow
* **Generation:** System compiles the clauses into a single PDF upon Booking.
* **Action:**
    * Sent to Client via Email/Portal.
    * Client clicks "Sign" (Simple E-Signature / Audit Trail).
    * Status updates to `Signed`.
* **Lock:** Once signed, the "Package Items" and "Price" are locked. Any changes require a "Contract Amendment" (New PDF).