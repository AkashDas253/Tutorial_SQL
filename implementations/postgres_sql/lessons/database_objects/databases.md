## PostgreSQL – Databases

### Overview

A **database** in PostgreSQL is a **collection of schemas, tables, indexes, functions, and other objects** that form a self-contained logical storage unit. Multiple databases can exist within a **single PostgreSQL cluster**, each isolated from the others.

### Key Concepts

* **Database Cluster**

  * A collection of **databases managed by a single PostgreSQL server instance**.
  * Each cluster has a shared `PGDATA` directory storing all data files, configurations, and WAL.
  * A cluster contains system databases like `postgres` and `template1`.

* **Database Creation**

  * `CREATE DATABASE` command creates a new database.
  * Template databases (usually `template1`) provide default objects and settings.
  * Each database has its own **namespace** and catalog tables.

* **Database Isolation**

  * Databases are **isolated from each other**.
  * No direct cross-database queries; require **FDW (Foreign Data Wrappers)** for access.
  * Separate connections are required for different databases.

* **System Databases**

  * **postgres**: Default maintenance database.
  * **template1**: Template for creating new databases.
  * **template0**: Clean template, cannot be modified; ensures fresh database creation.

* **Database Properties**

  * **Encoding / Character Set**: UTF8, LATIN1, etc.
  * **Locale / Collation**: Determines sorting and comparison rules.
  * **Connection Limits**: Maximum number of concurrent connections.
  * **Tablespace Assignment**: Optionally specify tablespaces for database storage.

* **Database Management**

  * **ALTER DATABASE**: Modify properties (e.g., name, owner, tablespace).
  * **DROP DATABASE**: Permanently deletes a database and all contained objects.
  * **Backup & Restore**:

    * `pg_dump` / `pg_restore`
    * `pg_basebackup` for full cluster backup

* **Privileges**

  * Managed using **roles and grants**.
  * Control who can connect, create objects, or perform administrative tasks.

### Summary

In PostgreSQL, a **database is the primary logical container** for all data objects. Multiple databases in a cluster provide **isolation, organization, and manageability**, while system databases facilitate template-based creation, maintenance, and administrative tasks.

---
