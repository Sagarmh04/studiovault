# Global Package Library (Template Engine)

## 1. Context
* **Goal:** Standardization without rigidity. HQ defines the "What" (Deliverables), Branch defines the "How Much" (Price).
* **Visibility Rule:** **Open Library.**
    * All published templates are visible to *all* branches.
    * We rely on Branch Manager competence to select relevant packages (e.g., ignoring "Beach Package" in a landlocked city).

## 2. The Workflow
* **Step 1: Creation (HQ)**
    * Admin creates "Master Template".
    * Defines Items: "8 Hours, 300 Photos, Drone".
    * Defines *Suggested* Price (Optional).
    * Action: `Publish to Library`.
* **Step 2: Import (Branch Level)**
    * Manager sees "New Templates" in Library.
    * Clicks **Import**.
    * System creates a *Local Copy* of the package.
    * Manager **MUST** set the Final Price and Tax Rate for their location.

## 3. The Sync Strategy (Notification Driven)
* **Scenario:** HQ updates the Master Template (e.g., adds "Free Album").
* **Logic:** System does **NOT** auto-update the Branch's local copy (to protect active contracts).
* **Notification:**
    * Branch Manager sees a badge: **"Update Available (v2)"** next to the package.
* **Action:**
    * Manager clicks to review changes ("Diff View").
    * Options:
        * `Accept Update`: Overwrites local attributes (Price might need re-confirmation).
        * `Ignore`: Keeps the local version as is.