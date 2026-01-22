# POS & Fast Booking Module (Walk-In)

## 1. Context & Scope
* **Target User:** Receptionist/Clerk (Offline).
* **Platform:** Strictly **Desktop Application** (Electron). Web version disables this feature.
* **Goal:** Speed. Zero latency.
* **Data Principle:** **Append Only.**
    * *Logic:* Offline transactions are strictly chronological. Edits are created as new "Correction Entries" rather than overwriting old ones to prevent sync conflicts. Deletion is allowed but logged as a "Voided Transaction".

## 2. The Interface Logic
* **Selector Toggle:**
    * *Condition:* Checks Inventory. If Merch exists -> Show "Merch | Photo Services" Toggle.
    * *Default:* "Photo Services".
* **Fast Packages (Non-Linear Pricing):**
    * *Logic:* Prices are **Pre-defined**, not calculated.
    * *Example:* "16 Passport" = ₹200. "32 Passport" = ₹350.
    * *Resource Check:* Hidden background check. Warns only if conflict exists.

## 3. The Print-to-Bill Workflow
* **Step 1: Package Selection.** Clerk selects "16 Passport Photos".
* **Step 2: Layout & Orientation.**
    * *Input:* User selects the physical cut/arrangement.
    * *Options (Dynamic):* "4x4 Grid", "8x2 Strip", "16x1 Strip".
    * *Preview:* Real-time visual representation of the paper output.
* **Step 3: Print Command.** User clicks "Print" -> App opens OS Print Dialog.
* **Step 4: Verification Loop.**
    * App asks: "Did the print complete successfully?"
    * *Yes:* Transaction is Billed. Revenue recorded.
    * *No:* Transaction cancelled (No revenue recorded).

## 4. Custom Billing (Ad-Hoc)
* **Custom Bill Button:** Allows manual entry of Service Name, Price Override, and Merch.
* **Inheritance:** "Included/Excluded" metadata from the base package is preserved even if price is manually changed.