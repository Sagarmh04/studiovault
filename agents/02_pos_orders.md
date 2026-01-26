# Flaw 1: Missing POS Module

## User Feedback
The PRD establishes a clear rule that walk-in Point-of-Sale (POS) transactions are distinct from standard project bookings. However, the initial schema was missing a dedicated table to store these `pos_orders`, creating a significant gap in the system's architecture.

## Resolution
To address this, I am introducing a new `pos_orders` table. This table is designed specifically to capture the essential details of a POS transaction, including the items sold, total amount, and payment method.

This ensures that the POS module has a dedicated and correctly structured home within the database, aligning the schema with the application's core requirements.

## Schema
```sql
CREATE TABLE pos_orders (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  total_amount REAL NOT NULL,
  items_json TEXT NOT NULL,
  payment_method TEXT,
  status TEXT NOT NULL, -- paid, voided, corrected
  created_at INTEGER NOT NULL
);
CREATE INDEX idx_pos_orders_branch_id_created_at
  ON pos_orders(branch_id, created_at);
```
