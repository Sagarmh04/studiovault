# Roles & Access Control (Atomic Unit)

## 1. Authentication Strategy
* **Method:** "Ghost Accounts" (Admin-created).
* **Identity:** `role.name@organization.in` (e.g., `clerk.blr@pixeldence.in`).
* **Password:** Set by Owner -> Reset by Staff on first login.

## 2. The Permission Matrix

| Feature | Owner | Manager | Clerk | Photographer | Accountant |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **POS (Walk-in)** | ✅ Full | ✅ Full | ✅ Full | ❌ | ❌ |
| **Bookings** | ✅ Full | ✅ Full | ✅ Create Only | 👁 View Assigned | ❌ |
| **Calendar** | ✅ Full | ✅ Full | 👁 View Only | 👁 View Assigned | ❌ |
| **Inventory** | ✅ Full | ✅ Full | 👁 View Availability | 👁 View Check-out | ❌ |
| **Finance (Revenue)** | ✅ Full | 👁 Report Only | ❌ | ❌ | 👁 View All |
| **Wallet/Payouts** | ✅ Full | ❌ | ❌ | ❌ | ❌ |
| **Settings** | ✅ Full | ❌ | ❌ | ❌ | ❌ |

## 3. Detailed Role Definitions

### A. The Clerk (Front Desk)
* **Primary UI:** Defaults to **POS / Fast Booking** screen on login.
* **Capabilities:**
    * Can create "Walk-in" bills.
    * Can create "Project" inquiries.
    * Can print Receipts.
* **Restrictions:**
    * Cannot **Delete** a bill (Must request Void from Manager).
    * Cannot see "Total Monthly Revenue".

### B. The Photographer / Editor
* **Primary UI:** Defaults to **My Tasks / Calendar**.
* **Capabilities:**
    * Access to "Smart Select" Desktop Bridge.
    * Can mark tasks as "Completed".
* **Restrictions:**
    * **Client Privacy:** Cannot see Client Phone/Email unless explicitly allowed per job.
    * **Financial Blindness:** Cannot see the value of the invoice.

### C. The Manager (Operational Lead)
* **Primary UI:** Dashboard Overview.
* **Capabilities:**
    * Can override "Price" in bookings.
    * Can Void/Refund transactions.
    * Can assign Staff to jobs.