## PostgreSQL – Storage Architecture

### Overview

PostgreSQL’s storage architecture defines how **data, indexes, and transaction logs** are stored on disk to ensure **durability, reliability, and performance**. It uses a **tablespace-based, page-oriented system** with write-ahead logging (WAL) for crash recovery.

### Tablespaces

* **Definition**: Locations on disk where database objects are stored.
* **Default Tablespace**: `pg_default` for regular objects, `pg_global` for shared objects.
* **Custom Tablespaces**:

  * Can be created per database or table.
  * Allows distributing data across multiple storage devices.
  * Useful for performance optimization or storage management.

### Data Files

* **Database Cluster**: All databases in a PostgreSQL instance reside in a single cluster directory (`PGDATA`).
* **File Structure**:

  * Each table or index is stored as one or more **relation files**.
  * Large tables split into multiple 1GB files internally.
* **File Types**:

  * **Heap files**: Store actual table rows.
  * **TOAST tables**: Store large column values (e.g., large text or JSON).
  * **Index files**: Store B-tree, GIN, GiST, or other index structures.
* **Physical Storage**:

  * 8KB pages (default) store tuples.
  * Each tuple contains header metadata (transaction IDs, visibility info) and actual data.

### Write-Ahead Logging (WAL)

* **Purpose**: Ensures durability and crash recovery.
* **Mechanism**:

  * All changes are first written to WAL before being applied to data files.
  * WAL files allow **replay of committed transactions** after a crash.
* **WAL Segments**:

  * Typically 16 MB each.
  * Stored in the `pg_wal` directory.
* **Checkpointing**:

  * Checkpoints write dirty pages from memory to disk.
  * Reduces WAL replay time on recovery.

### MVCC Support in Storage

* **Tuple Versioning**:

  * Each row has transaction IDs for visibility control.
  * Dead tuples are cleaned by **vacuum** processes.
* **Concurrency**:

  * Multiple versions allow readers to access old snapshots while writers update rows.

### Storage Maintenance

* **VACUUM**:

  * Removes dead tuples and recovers space.
* **ANALYZE**:

  * Collects statistics for query optimization.
* **REINDEX**:

  * Rebuilds indexes to maintain performance.
* **Tablespace Management**:

  * Move or add tablespaces without downtime.

### Summary

PostgreSQL storage architecture is **robust and scalable**, combining:

* Tablespaces for flexible disk management
* Page-oriented storage for efficiency
* WAL for durability
* MVCC for high-concurrency transaction handling

---
