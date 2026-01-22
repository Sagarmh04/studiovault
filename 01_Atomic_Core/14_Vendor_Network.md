# Vendor & Second Shooter Management

## 1. The "Mini-CRM"
* **Target:** Managing Freelancers, Makeup Artists, and Assistant Shooters who are *not* full-time employees.
* **Database Fields:**
    * Name & Contact.
    * **Role:** (e.g., "Candid Photographer", "Drone Operator").
    * **Day Rate:** (e.g., ₹5,000/day).
    * **Gear List:** (What equipment they bring).
    * **Internal Rating:** 1-5 Stars (Private notes: "Always late", "Great with kids").

## 2. Assignment Logic
* **Context:** Inside the "Job Card" (Crew Section).
* **Action:** Drag-and-drop Vendor from list.
* **Availability Check:**
    * System checks if this Vendor is assigned to *another* StudioVault project on the same day.
    * *Conflict:* Warns user, but allows override (since they are freelancers, they might manage their own schedule).

## 3. Financial Integration
* **Cost Tracking:** Assigning a Vendor adds their "Day Rate" to the **Project Expense** column.
* **Profit View:** `Project Revenue - (Vendor Cost + Asset Cost) = Estimated Profit`.