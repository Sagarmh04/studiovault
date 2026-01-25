# Agency Governance & Approval Engine

## 1. Context & Goal
* **Goal:** Replace "Blind Trust" with "Systematic Control".
* **The Problem:** In a multi-branch agency, a Manager could theoretically refund a ₹1,00,000 invoice to their own bank account or give a 100% discount to a friend.
* **The Solution:** A **Threshold-Based Approval System**. Actions below the threshold are instant; actions above require HQ Sign-off.

## 2. The Threshold Logic (The Rules)
* **Configuration:** HQ Owner sets these limits in `Global Settings`.
* **Triggers (Default Recommendations):**
    * **Discount Cap:** `IF Discount > 15%` -> **Require Approval**.
    * **Refund Cap:** `IF Refund_Amount > ₹5,000` -> **Require Approval**.
    * **Project Deletion:** `IF Project_Status == 'Signed'` -> **Require Approval**.
    * **Invoice Voiding:** `IF Invoice_Status == 'Paid'` -> **Require Approval**.

## 3. The Approval Workflow
* **Step 1: The Request (Branch Level)**
    * Manager tries to apply a 50% discount.
    * System blocks the action.
    * Modal appears: *"This exceeds your 15% limit. Request Approval?"*
    * Manager adds note: *"Family friend of the Owner."* -> Clicks Send.
    * **Status:** Transaction enters `PENDING_APPROVAL` state.
* **Step 2: The Decision (HQ Level)**
    * Owner receives Push Notification: *"Request: 50% Discount in Mumbai Branch."*
    * Owner clicks "Approve" or "Reject" (with comment).
* **Step 3: Execution (System Level)**
    * **If Approved:** The discount is applied immediately. Manager notified.
    * **If Rejected:** Transaction reverts to original price. Manager notified.

## 4. Emergency Overrides
* **The "Super Admin" Key:** The Organization Owner (User ID #1) is exempt from all thresholds.
* **Audit Trail:** Every Approval/Rejection is logged in the **Global Audit Log** with the approver's ID and timestamp.

## 5. Automated Enforcement (The "Smart Watermark" Rule)
* **Context:** Protecting revenue without manual checking.
* **Rule:** `IF Invoice_Balance > 0` -> **FORCE Watermark**.
* **Behavior:**
    * If a Manager tries to disable watermarking on an unpaid project, the system **Blocks** the action.
    * *Exception:* Manager can "Request Approval" to bypass (e.g., for a trusted corporate client).