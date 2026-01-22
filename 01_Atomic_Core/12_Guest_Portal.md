# Guest Experience Portal (QR Uploads)

## 1. Context
* **Problem:** Guests take thousands of candid photos/videos at weddings that the couple never sees.
* **Solution:** A frictionless, app-less upload portal for event guests.

## 2. The Workflow
* **Trigger:** Photographer clicks "Generate Event QR" inside a Project.
* **Output:** A printable PDF/Image (Tent Card format) containing the QR Code.
* **Guest Action:**
    1.  Scans QR (No App required).
    2.  Opens `studiovault.in/guest-upload/[project_id]`.
    3.  Uploads Photos/Videos.
    4.  (Optional) Enters Name/Wishes.

## 3. Storage & Management
* **Destination:** Files land in a segregated folder: `Project_X/Guest_Media/`.
* **Quarantine:** Files are visible to the Photographer *immediately* but must be "Approved" before appearing in the Client's Main Gallery.
* **Billing Impact:** **High Leverage.** These uploads count directly towards the User's Storage Quota.
    * *Logic:* More guest videos = Faster storage fill-up = User buys "Extra Storage" Add-on sooner.

## 4. Privacy
* **Scope:** Public Upload, Private View. Guests cannot see what others uploaded, only what *they* uploaded.