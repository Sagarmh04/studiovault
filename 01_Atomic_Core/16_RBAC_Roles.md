# Roles & Access Control (Atomic Unit)

## 1. Authentication Strategy
* **Method:** "Ghost Accounts" (Admin-created).
* **Naming Convention:**
    * **Prefix:** Custom defined by Admin (e.g., `sagar`, `reception`, `user1`).
    * **Suffix:** Fixed to Organization Domain (e.g., `@pixeldence.in`).
    * **Result:** `sagar@pixeldence.in`.
* **Credential Handling:** Admin sets Temp Password -> User resets on first login.

## 2. Role Composition (The "Multi-Hat" Logic)
* **Assignment:** Users are assigned an **Array of Roles** (e.g., `["Clerk", "Manager"]`).
* **Resolution Logic (The Union Rule):**
    * Permissions are **Additive**.
    * *Example:* If "Clerk" has `Finance: None` but "Manager" has `Finance: View`, the user gets `Finance: View`.
    * *Conflict:* If one role says "Edit" and another says "View", the **Highest Privilege** (Edit) wins.

## 3. The Core Permission Matrix (Atomic)
*These are the Fixed System Roles required for basic studio operations.*

| Feature               | Owner  | Manager        | Clerk                | Photographer      | Accountant  |
| :-------------------- | :----- | :------------- | :------------------- | :---------------- | :---------- |
| **POS (Walk-in)**     | ✅ Full | ✅ Full         | ✅ Full               | ❌                 | ❌           |
| **Bookings**          | ✅ Full | ✅ Full         | ✅ Create Only        | 👁 View Assigned  | ❌           |
| **Calendar**          | ✅ Full | ✅ Full         | 👁 View Only         | 👁 View Assigned  | ❌           |
| **Inventory**         | ✅ Full | ✅ Full         | 👁 View Availability | 👁 View Check-out | ❌           |
| **Finance (Revenue)** | ✅ Full | 👁 Report Only | ❌                    | ❌                 | 👁 View All |
| **Settings**          | ✅ Full | ❌              | ❌                    | ❌                 | ❌           |

## 4. Future Extensibility: The Roles Engine
* **Status:** PENDING / FUTURE SCOPE.
* **Concept:** A dynamic engine to create Custom Roles (e.g., "Marketing Staff", "Intern").
* **Constraint:** Not included in Phase 1 Atomic Core to avoid complexity. Will be defined after the Notification/Marketing modules are built.