## PostgreSQL Concepts Overview

### Basics

* Introduction

  * What is PostgreSQL
  * Features
  * Editions and versions
* Installation & Setup

  * OS-specific installation
  * Configuration files (postgresql.conf, pg\_hba.conf)
  * Starting/stopping server
  * Environment variables

### Architecture

* Process Architecture

  * Postmaster process
  * Backend processes
  * WAL writer, Checkpointer
* Storage Architecture

  * Tablespaces
  * Data files
  * Write-ahead logging (WAL)
* Transaction Management

  * ACID properties
  * MVCC (Multi-Version Concurrency Control)
* Memory & Caching

  * Shared buffers
  * Work memory
  * Temp buffers
* Query Processing

  * Query planner & optimizer
  * Execution engine
  * Caching

### Database Objects

* Databases
* Schemas
* Tables

  * Columns & data types
  * Constraints
* Views
* Indexes

  * B-tree, Hash, GiST, GIN, BRIN
* Sequences
* Materialized Views
* Functions

  * SQL functions
  * PL/pgSQL
  * Procedural languages
* Triggers
* Rules
* Extensions
* Domains
* Enumerated Types
* Foreign Tables (FDW)

### Data Types

* Numeric types
* Character types
* Boolean
* Date & Time types
* Arrays
* JSON / JSONB
* UUID
* Geometric types
* Network types (INET, CIDR, MACADDR)
* Range types
* Composite types
* XML

### Constraints

* Primary Key
* Foreign Key
* Unique
* Check
* Not Null
* Exclusion constraints

### Indexing & Performance

* Index types
* Partial indexes
* Expression indexes
* Covering indexes
* Index-only scans
* Index maintenance
* VACUUM / ANALYZE
* Query tuning

### SQL & Querying

* Data Manipulation (DML)

  * SELECT
  * INSERT
  * UPDATE
  * DELETE
* Data Definition (DDL)

  * CREATE / ALTER / DROP
  * Table alterations
  * Schema alterations
* Transaction Control

  * BEGIN / COMMIT / ROLLBACK
  * SAVEPOINT
  * Transaction isolation levels
* Joins

  * INNER, LEFT, RIGHT, FULL
  * CROSS JOIN
  * SELF JOIN
* Set Operations

  * UNION / INTERSECT / EXCEPT
* Subqueries

  * Correlated
  * Non-correlated
* Window Functions
* CTEs (Common Table Expressions)

  * Recursive
* Aggregates
* Grouping Sets / Rollup / Cube
* JSON Functions & Operators

### Procedural & Advanced SQL

* PL/pgSQL

  * Variables & constants
  * Control structures (IF, CASE, LOOP)
  * Cursors
  * Exception handling
* Other Procedural Languages

  * PL/Python, PL/Perl, PL/Tcl, PL/Java
* Triggers & Trigger Functions
* Rules

### Security & Roles

* Roles & Users

  * Superuser vs normal user
  * Role inheritance
* Privileges

  * GRANT / REVOKE
* Row-Level Security
* Authentication Methods

  * Password, MD5, SCRAM
  * GSSAPI, SSPI
* SSL / TLS

### Backup & Restore

* pg\_dump / pg\_restore
* pg\_basebackup
* PITR (Point-In-Time Recovery)
* WAL Archiving

### Replication & High Availability

* Streaming Replication
* Logical Replication
* Physical Replication
* Hot Standby
* Failover & Switchover
* Replication Slots

### Partitioning

* Table Partitioning

  * Range
  * List
  * Hash
* Inheritance-based partitioning
* Declarative Partitioning
* Partition Pruning

### Concurrency & Locking

* Locks

  * Row-level, Table-level, Advisory
* Deadlocks
* MVCC internals
* Isolation Levels

  * Read Uncommitted, Read Committed, Repeatable Read, Serializable

### Monitoring & Maintenance

* pg\_stat views
* Logging
* EXPLAIN / EXPLAIN ANALYZE
* VACUUM / VACUUM FULL
* REINDEX
* ANALYZE
* Auto-vacuum
* pg\_stat\_statements

### Extensions & Advanced Features

* PostGIS (Geospatial)
* Full Text Search
* Hstore
* Foreign Data Wrappers (FDW)
* TimescaleDB / other extensions

### Networking & Connections

* Client-Server communication
* Connection pooling

  * pgBouncer
  * pgpool-II
* Listen / Notify
* libpq & drivers

### Miscellaneous

* Temporary tables
* Unlogged tables
* Inheritance
* Arrays & composite types
* ENUM types
* Custom types & operators
* Event triggers
* Configuration tuning
* Logging & auditing

---
