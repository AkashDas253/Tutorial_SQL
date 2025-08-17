## PostgreSQL – Memory & Caching

### Overview

PostgreSQL uses **memory structures and caching mechanisms** to optimize query performance, reduce disk I/O, and manage resources for concurrent transactions. Proper tuning of memory settings is critical for database efficiency.

### Shared Memory

* **Shared Buffers**

  * Primary cache for table and index data.
  * Stores **frequently accessed pages** in memory.
  * Size configurable via `shared_buffers` in `postgresql.conf`.
* **WAL Buffers**

  * Temporarily stores Write-Ahead Log records before writing to disk.
  * Size controlled via `wal_buffers`.
* **Lock Tables**

  * Stores information about **locks** for concurrency control.
* **Session/Process Communication**

  * Shared memory enables communication between **backend and background processes**.

### Process-Local Memory

* **Work Memory (`work_mem`)**

  * Allocated per operation (sort, hash join, aggregation) in a query.
  * Determines **in-memory processing capacity** for each query operation.
* **Maintenance Memory (`maintenance_work_mem`)**

  * Used for **vacuuming, index creation, ALTER TABLE, and other maintenance tasks**.
* **Temp Buffers**

  * For temporary tables, per-session allocation.

### Caching Mechanisms

* **Buffer Cache**

  * PostgreSQL keeps **pages read from disk** in shared buffers.
  * Reduces repetitive disk reads for hot data.
* **OS File System Cache**

  * PostgreSQL relies on the OS to cache disk pages not in shared buffers.
* **Query Plan Caching**

  * Prepared statements can cache execution plans for repeated queries.
* **Index Caching**

  * Frequently accessed index pages are cached in memory to speed up lookups.

### Memory Management Considerations

* **Concurrency**

  * Each backend process consumes its own memory allocations.
  * High connection count increases total memory usage.
* **Autovacuum Memory Usage**

  * Autovacuum workers use `maintenance_work_mem`.
* **Temporary Operations**

  * Large sorts or joins may spill to disk if `work_mem` is insufficient.
* **Tuning Parameters**

  * `shared_buffers`: usually 25-40% of total RAM.
  * `work_mem`: sized per operation to avoid disk spills.
  * `maintenance_work_mem`: larger values speed up maintenance tasks.

### Summary

PostgreSQL uses a **multi-layered memory architecture**:

* **Shared memory** for caching frequently accessed data and coordinating processes.
* **Process-local memory** for query operations and maintenance.
* Efficient caching reduces disk I/O, improves query performance, and supports high concurrency.

---
