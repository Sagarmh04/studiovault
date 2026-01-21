# Agency Hierarchy & Inheritance

## 1. Structure
* **Organization:** The Parent Entity.
* **Branch:** The Child Entity. (Has unique Subdomain, Address, Tax ID).

## 2. Package Inheritance
* **Master Packages:** Created by Org Admin.
* **Branch Behavior:**
    * *Inherit:* Branch sees the Master Package.
    * *Override:* Branch can change **Price** and **Tax** only.
    * *Constraint:* Branch *cannot* change Core Attributes (e.g., "8 Hours") to ensure Brand Consistency.
    * *Custom:* Branch can create their own "Local Packages" visible only to them.

## 3. Resource Sharing (Future Scope)
* **Global Asset List:** Admins can view assets across all branches.
* **Transfer Logic:**
    * "Branch A" initiates Transfer of "Lens X" to "Branch B".
    * Asset Status: `In Transit` (Cannot be booked by anyone).
    * "Branch B" confirms receipt -> Asset moves to Branch B's Inventory.