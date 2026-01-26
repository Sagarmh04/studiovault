# Flaw 2 & 3: Package Versioning and Simplified Taxes

## User Feedback
### 2. Packages need stronger typing + versioning
The PRD specifies a system of master package templates and local, versioned copies for branches. The initial schema lacked fields to represent this hierarchy (`master_package_id`, `package_version`, `is_template`), which would make package governance impossible to implement.

### 3. Taxes are too simplified
The `tax_rate REAL NOT NULL` field was not flexible enough for global tax scenarios (e.g., split GST, VAT categories). The PRD called for modular tax adapters, and the schema needed to reflect this by using a more flexible format like JSON.

## Resolution
I am addressing both of these critical flaws by recreating the `packages` table with an improved schema.

1.  **Versioning:** I'm adding `master_package_id`, `package_version`, and `is_template` columns to enable the template/copy and versioning logic described in the PRD.
2.  **Modular Taxes:** I am replacing the rigid `tax_rate` column with a flexible `tax_json` TEXT field. This allows for storing complex tax structures and adapts to various international tax laws.

These changes make the `packages` table robust, scalable, and aligned with the business logic.

## Schema
```sql
CREATE TABLE packages (
  id TEXT PRIMARY KEY,
  branch_id TEXT NOT NULL REFERENCES branches(id),
  master_package_id TEXT, -- Link to the master template
  name TEXT NOT NULL,
  type TEXT,
  price REAL NOT NULL,
  tax_json TEXT, -- Replaces tax_rate
  inclusions_json TEXT,
  exclusions_json TEXT,
  resource_hooks_json TEXT,
  package_version INTEGER DEFAULT 1, -- Version number
  is_template BOOLEAN DEFAULT 0, -- Flag for master templates
  version INTEGER DEFAULT 1
);

CREATE INDEX idx_packages_branch_id ON packages(branch_id);
CREATE INDEX idx_packages_master_package_id ON packages(master_package_id);
```
