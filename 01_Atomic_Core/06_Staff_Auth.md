# Staff Authentication & Onboarding

## 1. The "Ghost" Account Problem
* **Scenario:** Agencies want to create logins for employees (e.g., `sagar@pixeldence.in`) without actually buying the email domain.
* **Constraint:** Standard "Email Verification" links will fail because the inbox doesn't exist.

## 2. The Solution: Admin-Created Flow
* **Action:** Agency Owner clicks "Add Staff" -> Enters Name, Role, and "Internal ID/Email".
* **Backend Logic:**
    1.  System calls Auth Provider (Cognito/Auth0) with `MessageAction = "SUPPRESS"` (No email sent).
    2.  System manually sets a **Temporary Password**.
* **UI Feedback:** Dashboard shows: "User Created. Temporary Password: `Pixel@123`. Please share this with Sagar."
* **First Login:** Employee logs in with Temp Password -> System forces immediate Password Change.

## 3. Password Recovery for "Ghost" Users
* **Workflow:** Employee forgets password.
* **Action:** Employee asks Manager.
* **Manager Action:** Admin Dashboard -> Team -> Select User -> Click "Reset Password".
* **Result:** System generates new Temp Password for Manager to share.