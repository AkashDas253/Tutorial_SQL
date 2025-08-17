## PostgreSQL – Indexing

### Overview

An **index** in PostgreSQL is a **database object that improves query performance** by allowing faster lookup of rows in a table. Indexes reduce the need for **full table scans** and are crucial for large datasets.

### Key Concepts

* **Purpose**

  * Speed up **SELECT queries**, joins, and ORDER BY operations.
  * Enforce **uniqueness** constraints (PRIMARY KEY, UNIQUE).
  * Optimize aggregate queries and filtering.

* **Types of Indexes**

  * **B-Tree** (default)

    * Efficient for equality and range queries (`=`, `<`, `>`, `<=`, `>=`).
  * **Hash**

    * Optimized for equality comparisons.
    * Less versatile than B-Tree.
  * **GIN (Generalized Inverted Index)**

    * Suitable for **array, JSONB, and full-text search**.
    * Supports multi-valued fields efficiently.
  * **GiST (Generalized Search Tree)**

    * Supports geometric and full-text data, and custom operator classes.
  * **SP-GiST (Space-Partitioned GiST)**

    * Efficient for **multi-dimensional data**, like quadtrees or k-d trees.
  * **BRIN (Block Range Index)**

    * Lightweight index for **large, sequentially ordered datasets**.
    * Stores summary information for block ranges instead of each row.

* **Index Variants**

  * **Unique Index**

    * Enforces uniqueness on one or more columns.
  * **Partial Index**

    * Indexes only a subset of rows that satisfy a condition.
  * **Expression Index**

    * Indexes the result of an expression rather than a column directly.
  * **Covering Index (INCLUDE)**

    * Stores additional columns in the index for **index-only scans**.

* **Index Creation & Management**

  * `CREATE INDEX index_name ON table_name (column(s)) [USING index_type]`
  * `CREATE UNIQUE INDEX` – Enforce uniqueness.
  * `ALTER INDEX` – Rename, reindex, or modify storage parameters.
  * `DROP INDEX` – Remove an index.
  * `REINDEX` – Rebuild an index to optimize performance.

* **Usage**

  * Automatically used by the **query planner** when beneficial.
  * Improves performance for:

    * WHERE clauses
    * JOINs
    * ORDER BY and DISTINCT queries
    * Aggregate functions
  * Index-only scans are possible if **all requested columns are in the index**.

* **Maintenance**

  * Regular **VACUUM** and **ANALYZE** ensure optimal performance.
  * Large inserts/updates may require **reindexing** to avoid fragmentation.

* **Considerations**

  * Indexes consume additional **disk space**.
  * Excessive or unnecessary indexes can **slow down write operations** (INSERT/UPDATE/DELETE).
  * Choice of index type depends on **query patterns and data distribution**.

### Summary

Indexing in PostgreSQL is a **key optimization tool**:

* Supports B-Tree, Hash, GIN, GiST, SP-GiST, BRIN for different use cases
* Variants include unique, partial, expression, and covering indexes
* Proper use ensures **fast data retrieval** while maintaining data integrity

---
