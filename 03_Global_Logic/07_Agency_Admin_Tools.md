# Agency Admin Tools (Resources & Payroll)

## 1. Visual Studio Booking
* **Context:** Booking physical spaces (Floors, Sets) inside the agency.
* **UI Pattern:** **Rich Card Grid** (Not Map).
* **Card Data:**
    * Thumbnail Image.
    * Zone Name (e.g., "Green Screen Floor").
    * Capacity & Dimensions.
    * "Included Gear" list.
* **Flow:** Select Zone -> View Availability Calendar -> Reserve Slot.

## 2. Payroll & Commission Engine (Human-in-the-Loop)
* **Goal:** Calculate variable pay without blind automation errors.
* **The "Draft" Workflow:**
    1.  **Auto-Compute:** System calculates `Base Salary` + `Session Fees` + `Commission %` (from approved Invoices).
    2.  **Draft Generation:** Creates a "Provisional Payslip" on the 1st of the month.
    3.  **Admin Review:**
        * Manager opens the Draft.
        * *Action:* Add "Bonus" or "Deduction" (Manual Entry).
    4.  **Approval:** Manager clicks "Finalize".
        * *Result:* Amount is locked and recorded as an "Expense" in the Finance Module.

## 3. Resource Management 2.0 (The Shift Planner)
* **Goal:** Managing Staff availability across a large team.
* **The Roster View:** Weekly Calendar Grid (Rows = Staff, Cols = Days).
* **Capabilities:**
    * **Leave Management:** Mark Staff as `On Leave` / `Sick`.
        * *Impact:* System blocks them from being assigned to new jobs on those days.
    * **Freelancer Slots:** Mark days where "Freelancer X" is booked to come in.
    * **Utilization Heatmap:** Visual color coding to see who is overworked (Red) or underutilized (Green).