# Flaw 9: Missing Org-Level Finance Settings

## User Feedback
The PRD mentions a "Global finance settings" module, including expense inputs. However, the initial schema had no table to store this crucial financial data, leaving a gap in the application's ability to track organizational expenses.

## Resolution
To address this, I am introducing a new `expenses` table. This table allows for the recording of expenses at the branch level, capturing the label, amount, and creation date. This is a foundational step towards building the global finance module.

## Schema
```sql
CREATE TABLE expenses (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  label TEXT NOT NULL,
  amount REAL NOT NULL,
  created_at INTEGER NOT NULL
);
```
