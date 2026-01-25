Lifecycle Events & Data Retention

## 1. Downgrade Logic (The "Overage" Trap)

**Scenario:**
User has 60GB used (Paid Plan) → Downgrades to Free (2GB limit)

**Immediate State:**
Account marked `Over_Limit`

**Consequences:**
1. Upload Block: No new files can be uploaded
2. Client Lock: Delivery portals for old projects are paused
   (Client sees: "Gallery Temporarily Unavailable")
3. Grace Period: User has 14 days to delete excess data

---

## 2. Deletion & Archival

**Manual Delete:**
User selects "Delete Project"
- Moved to Trash for 30 days (Recoverable)
- Then Hard Delete

**Auto-Delete Timer (User Configurable):**
- Example: "Auto-delete RAW files 6 months after Project Completion"
- System executes deletion to control storage usage and costs

---

## 3. Billing Disputes & Refund Policy (No Wallet)

StudioVault does not maintain stored balances or wallet refunds.

**Subscription Policy:**
- Monthly or Annual billing (annual includes discount)
- No refunds once billed, except where required by law

**Overdue Enforcement:**
- 7-day grace period after invoice due date
- After grace period:
  - Uploads blocked
  - Delivery portals frozen

**Data Non-Payment Timeline:**
- Day 45: Final warning + One-click Export ZIP offered
- Day 60: Storage eligible for deletion if unpaid

All policies are explicitly defined in Terms and Compliance rules.
