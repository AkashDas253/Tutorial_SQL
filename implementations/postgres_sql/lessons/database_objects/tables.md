## PostgreSQL – Tables

### Overview

A **table** is the **core data storage object** in PostgreSQL. It stores **rows (tuples) and columns (attributes)**, with each table belonging to a schema. Tables are the foundation for all database operations, including querying, updating, and indexing.

### Key Concepts

* **Table Structure**

  * **Columns**: Define the attributes with specific data types.
  * **Rows/Tuples**: Store actual data values.
  * **System Columns**: PostgreSQL automatically adds system columns like `ctid`, `xmin`, `xmax`, and `cmax` for MVCC and internal tracking.

* **Table Types**

  * **Permanent Tables**

    * Standard tables stored on disk permanently.
  * **Temporary Tables**

    * Exists only for the session or transaction.
    * Stored in `pg_temp` schema; automatically dropped at session end.
  * **Unlogged Tables**

    * Bypass WAL, faster writes but not crash-safe.
  * **Foreign Tables**

    * Represent tables in external databases via **FDW (Foreign Data Wrappers)**.

* **Column Definitions**

  * Name and data type
  * Default values
  * Constraints (NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK)
  * Collation (for string comparison and sorting)

* **Constraints**

  * **Primary Key**: Uniquely identifies each row.
  * **Foreign Key**: Enforces referential integrity with another table.
  * **Unique**: Ensures column values are unique.
  * **Check**: Enforces custom conditions.
  * **Not Null**: Disallows NULL values.
  * **Exclusion Constraint**: Ensures uniqueness based on an operator.

* **Table Inheritance**

  * Tables can inherit columns and constraints from **parent tables**.
  * Useful for partitioning and modeling hierarchical data.

* **Partitioned Tables**

  * Logical table split into multiple **child tables** (partitions) based on key values.
  * Types: Range, List, Hash.
  * Improves query performance on large datasets.

* **Table Management**

  * `CREATE TABLE` – Define a new table.
  * `ALTER TABLE` – Modify structure or constraints.
  * `DROP TABLE` – Delete a table permanently.
  * `TRUNCATE` – Quickly remove all rows without logging individual deletions.

* **Storage**

  * Stored as **heap files** on disk.
  * Rows are stored in **pages (default 8KB)**.
  * Large values stored in **TOAST tables** for out-of-line storage.

* **Indexes**

  * Optional structures to speed up queries.
  * Can be defined per table on one or more columns.

### Summary

Tables in PostgreSQL are **the primary storage objects** supporting:

* Structured data storage with rows and columns
* Constraints for data integrity
* Partitioning and inheritance for advanced organization
* Optimized storage and indexing for performance

---
