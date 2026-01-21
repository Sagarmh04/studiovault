# POS & Fast Booking Module (Walk-In)

## 1. Context & Scope
* **Target User:** Receptionist/Clerk (Offline).
* **Platform:** Strictly **Desktop Application** (Electron). Web version disables this feature.
* **Goal:** Speed. Zero latency between "Customer Request" and "Billing".

## 2. The Interface Logic
* **Selector Toggle:**
    * *Condition:* Checks Inventory. If Merch exists -> Show "Merch | Photo Services" Toggle.
    * *Default:* "Photo Services".
* **Fast Packages (Quantity-Based):**
    * Distinct from "Time-Based" Project Packages.
    * *Structure:* `Name: 16 Passport`, `Qty: 16`, `Paper: 4x6`, `Price: ₹200`.
    * *Resource Check:* Hidden background check (e.g., "Is Studio Camera Free for next 15 mins?"). Warns only if conflict exists.

## 3. The Print-to-Bill Workflow
* **Step 1:** Clerk selects "16 Passport Photos".
* **Step 2:** App generates a Print Sheet (Grid layout).
* **Step 3:** User clicks "Print" -> App opens OS Print Dialog.
* **Step 4:** **Verification Loop.**
    * App asks: "Did the print complete successfully?"
    * *Yes:* Transaction is Billed. Revenue recorded.
    * *No:* Transaction cancelled (No revenue recorded).

## 4. Custom Billing (Ad-Hoc)
* **Custom Bill Button:** Allows manual entry of:
    * Service Name ("Custom Restoration").
    * Price Override (e.g., ₹200 -> ₹180).
    * Merch Items (if enabled).