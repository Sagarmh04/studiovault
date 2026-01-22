# Pending & Deferred Scope (Atomic Phase)

## 1. Advanced Roles Engine
* **Deferred Item:** Definition of "Marketing Staff" and "Custom Role" capabilities.
* **Reason:** Dependent on the Marketing/Notification module which is not yet designed.
* **Next Step:** Design this during the "Agency/Complex" phase.

## 2. Offline Data Versioning
* **Deferred Item:** Logic for syncing offline POS data without full-file scanning (Delta Sync).
* **Reason:** High technical complexity; requires stable data schema first.
* **Next Step:** Technical Architecture phase.

## 3. Local AI Culling
* **Deferred Item:** Client-side ML models for "Blink Detection" and "Focus Score".
* **Reason:** High engineering effort; classified as Phase 2 "Moat" feature.
## 4. Atomic Phase (Deferred)
* **Advanced Roles Engine:** Custom roles (Marketing, Intern).
* **Offline Data Versioning:** Delta Sync for POS.
* **Local AI Culling:** Desktop ML models.

## 5. Agency Phase (Deferred / To Be Deep Dived)
* **Asset Maintenance (Service Logs):**
    * *Status:* DEFERRED.
    * *Requirement:* Tracking "Service History" of lenses and auto-blocking gear based on usage hours.
    * *Reason:* Complexity risk. Manual "Mark as Damaged" is sufficient for Phase 1.
* **The Approval Engine:** (HQ approving refunds).
* **Staff Roaming:** (Assigning Branch A staff to Branch B).
* **Custom Domain:** (White-labeling).