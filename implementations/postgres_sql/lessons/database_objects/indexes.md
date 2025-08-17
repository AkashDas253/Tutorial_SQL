## PostgreSQL – Indexes

### Overview

An **index** in PostgreSQL is a **database object that improves query performance** by allowing faster retrieval of rows from a table. Indexes are optional but essential for **efficient search, join, and sorting operations** on large datasets.

### Key Concepts

* **Purpose**

  * Speed up data retrieval.
  * Reduce the need for full table scans.
  * Support uniqueness constraints (e.g., PRIMARY KEY, UNIQUE).

* **Index Types**

  * **B-Tree**

    * Default index type.
    * Efficient for equality and range queries (`=`, `<`, `<=`, `>`, `>=`).
  * **Hash**

    * Optimized for equality comparisons only.
    * Faster than B-Tree for simple equality but less versatile.
  * **GiST (Generalized Search Tree)**

    * Supports complex data types and similarity searches (e.g., geometric, full-text, range types).
  * **GIN (Generalized Inverted Index)**

    * Optimized for indexing **composite values** like arrays, JSONB, and full-text search.
  * **BRIN (Block Range Index)**

    * Lightweight, efficient for **large, sequentially ordered datasets**.
  * **SP-GiST**

    * Supports space-partitioned data structures (quadtrees, k-d trees) for multidimensional data.

* **Index Variants**

  * **Unique Index**

    * Ensures no duplicate values exist in the indexed column(s).
  * **Partial Index**

    * Indexes a **subset of rows** based on a condition.
  * **Expression Index**

    * Indexes the result of an expression instead of a column directly.
  * **Covering Index (INCLUDE)**

    * Stores additional columns in the index for **index-only scans**.

* **Index Creation & Management**

  * `CREATE INDEX index_name ON table_name (column(s))`
  * `CREATE UNIQUE INDEX index_name ON table_name (column(s))`
  * `ALTER INDEX` – Rename, reindex, or set storage parameters.
  * `DROP INDEX` – Remove an index.
  * `REINDEX` – Rebuild an index to remove fragmentation.

* **Index Usage**

  * The query planner **decides whether to use an index** based on cost estimation and statistics.
  * Indexes can be used for **joins, WHERE clauses, ORDER BY, DISTINCT**, and aggregation optimizations.
  * Index-only scans avoid accessing table data if all required columns are in the index.

* **Maintenance**

  * Regular **VACUUM** and **ANALYZE** to maintain performance.
  * Large updates or inserts may require **reindexing** for optimal performance.

### Summary

Indexes in PostgreSQL are **critical for query performance**:

* B-Tree, Hash, GiST, GIN, BRIN, and SP-GiST support different data types and query patterns
* Variants like unique, partial, and expression indexes enhance flexibility
* Proper maintenance ensures **efficient retrieval and storage**

---
