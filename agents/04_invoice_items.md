# Flaw 4: Invoices Lack Line Items

## User Feedback
The initial `invoices` table had a fatal flaw for any accounting system: it only stored a total amount (`amount_total`). It lacked the concept of line items, making it impossible to answer basic questions like "What was sold?" or to handle disputes and partial refunds properly. The schema was not fit for purpose.

## Resolution
To fix this, I am introducing a new `invoice_items` table. This table will store individual line items for each invoice, including a description, quantity, unit price, and its own flexible `tax_json`. This provides the necessary granularity for accurate accounting, auditing, and financial operations.

This change is fundamental to making the finance module viable.

## Schema
```sql
CREATE TABLE invoice_items (
  id TEXT PRIMARY KEY,
  invoice_id TEXT NOT NULL REFERENCES invoices(id),
  item_type TEXT NOT NULL, -- service, merch
  description TEXT NOT NULL,
  qty INTEGER DEFAULT 1,
  unit_price REAL NOT NULL,
  tax_json TEXT,
  total REAL NOT NULL
);
CREATE INDEX idx_invoice_items_invoice_id ON invoice_items(invoice_id);
```
