## PostgreSQL

### Notes Specific
- [Concepts](lessons/concepts/readme.md)
- [Documentation](https://www.postgresql.org/docs/)

### Basics

- [Introduction](lessons/introduction/readme.md)
  <!-- - [What is PostgreSQL](lessons/introduction/what_is_postgresql.md)
  - [Features](lessons/introduction/features.md)
  - [Editions and versions](lessons/introduction/editions_versions.md) -->
- [Installation & Setup](lessons/installation_setup/readme.md)
  <!-- - [OS-specific installation](lessons/installation_setup/os_specific.md)
  - [Configuration files](lessons/installation_setup/config_files.md)
  - [Starting/stopping server](lessons/installation_setup/server_control.md)
  - [Environment variables](lessons/installation_setup/env_vars.md) -->

### Architecture

- [Process Architecture](lessons/architecture/process_architecture.md)
  <!-- - [Postmaster process](lessons/architecture/postmaster.md)
  - [Backend processes](lessons/architecture/backend_processes.md)
  - [WAL writer, Checkpointer](lessons/architecture/wal_writer_checkpointer.md) -->
- [Storage Architecture](lessons/architecture/storage_architecture.md)
  <!-- - [Tablespaces](lessons/architecture/tablespaces.md)
  - [Data files](lessons/architecture/data_files.md)
  - [Write-ahead logging (WAL)](lessons/architecture/wal.md) -->
- [Transaction Management](lessons/architecture/transaction_management.md)
  <!-- - [ACID properties](lessons/architecture/acid.md)
  - [MVCC](lessons/architecture/mvcc.md) -->
- [Memory & Caching](lessons/architecture/memory_caching.md)
  <!-- - [Shared buffers](lessons/architecture/shared_buffers.md)
  - [Work memory](lessons/architecture/work_memory.md)
  - [Temp buffers](lessons/architecture/temp_buffers.md) -->
- [Query Processing](lessons/architecture/query_processing.md)
  <!-- - [Query planner & optimizer](lessons/architecture/query_planner_optimizer.md)
  - [Execution engine](lessons/architecture/execution_engine.md)
  - [Caching](lessons/architecture/caching.md) -->

### Database Objects

- [Databases](lessons/database_objects/databases.md)
- [Schemas](lessons/database_objects/schemas.md)
- [Tables](lessons/database_objects/tables.md)
  <!-- - [Columns & data types](lessons/database_objects/columns_data_types.md)
  - [Constraints](lessons/database_objects/constraints.md) -->
- [Views](lessons/database_objects/views.md)
- [Indexes](lessons/database_objects/indexes.md)
  <!-- - [B-tree, Hash, GiST, GIN, BRIN](lessons/database_objects/index_types.md) -->
- [Sequences](lessons/database_objects/sequences.md)
- [Materialized Views](lessons/database_objects/materialized_views.md)
- [Functions](lessons/database_objects/functions.md)
  <!-- - [SQL functions](lessons/database_objects/sql_functions.md)
  - [PL/pgSQL](lessons/database_objects/plpgsql.md)
  - [Procedural languages](lessons/database_objects/procedural_languages.md) -->
- [Triggers](lessons/database_objects/triggers.md)
- [Rules](lessons/database_objects/rules.md)
- [Extensions](lessons/database_objects/extensions.md)
- [Domains](lessons/database_objects/domains.md)
- [Enumerated Types](lessons/database_objects/enumerated_types.md)
- [Foreign Tables (FDW)](lessons/database_objects/foreign_tables.md)

### Data Types

- [Datatypes](lessons/data_types/overview.md)
<!-- - [Numeric types](lessons/data_types/numeric.md)
- [Character types](lessons/data_types/character.md)
- [Boolean](lessons/data_types/boolean.md)
- [Date & Time types](lessons/data_types/date_time.md)
- [Arrays](lessons/data_types/arrays.md)
- [JSON / JSONB](lessons/data_types/json.md)
- [UUID](lessons/data_types/uuid.md)
- [Geometric types](lessons/data_types/geometric.md)
- [Network types](lessons/data_types/network.md)
- [Range types](lessons/data_types/range.md)
- [Composite types](lessons/data_types/composite.md)
- [XML](lessons/data_types/xml.md) -->

### Constraints

- [Constraints](lessons/constraints/overview.md)
<!-- - [Primary Key](lessons/constraints/primary_key.md)
- [Foreign Key](lessons/constraints/foreign_key.md)
- [Unique](lessons/constraints/unique.md)
- [Check](lessons/constraints/check.md)
- [Not Null](lessons/constraints/not_null.md)
- [Exclusion constraints](lessons/constraints/exclusion.md) -->

### Indexing & Performance

- [Index](lessons/indexing/index.md)
<!-- - [Index types](lessons/indexing/index_types.md)
- [Partial indexes](lessons/indexing/partial.md)
- [Expression indexes](lessons/indexing/expression.md)
- [Covering indexes](lessons/indexing/covering.md)
- [Index-only scans](lessons/indexing/index_only_scans.md)
- [Index maintenance](lessons/indexing/maintenance.md)
- [VACUUM / ANALYZE](lessons/indexing/vacuum_analyze.md)
- [Query tuning](lessons/indexing/query_tuning.md) -->

### SQL & Querying

- [Data Manipulation (DML)](lessons/sql/dml.md)
  - [SELECT](lessons/sql/select.md)
  - [INSERT](lessons/sql/insert.md)
  - [UPDATE](lessons/sql/update.md)
  - [DELETE](lessons/sql/delete.md)
- [Data Definition (DDL)](lessons/sql/ddl.md)
  - [CREATE / ALTER / DROP](lessons/sql/create_alter_drop.md)
  - [Table alterations](lessons/sql/table_alterations.md)
  - [Schema alterations](lessons/sql/schema_alterations.md)
- [Transaction Control](lessons/sql/transaction_control.md)
  - [BEGIN / COMMIT / ROLLBACK](lessons/sql/begin_commit_rollback.md)
  - [SAVEPOINT](lessons/sql/savepoint.md)
  - [Transaction isolation levels](lessons/sql/isolation_levels.md)
- [Joins](lessons/sql/joins.md)
  - [INNER, LEFT, RIGHT, FULL](lessons/sql/joins_types.md)
  - [CROSS JOIN](lessons/sql/cross_join.md)
  - [SELF JOIN](lessons/sql/self_join.md)
- [Set Operations](lessons/sql/set_operations.md)
  - [UNION / INTERSECT / EXCEPT](lessons/sql/union_intersect_except.md)
- [Subqueries](lessons/sql/subqueries.md)
  - [Correlated](lessons/sql/correlated_subqueries.md)
  - [Non-correlated](lessons/sql/non_correlated_subqueries.md)
- [Window Functions](lessons/sql/window_functions.md)
- [CTEs (Common Table Expressions)](lessons/sql/ctes.md)
  - [Recursive](lessons/sql/recursive_ctes.md)
- [Aggregates](lessons/sql/aggregates.md)
- [Grouping Sets / Rollup / Cube](lessons/sql/grouping_sets.md)
- [JSON Functions & Operators](lessons/sql/json_functions_operators.md)

<!-- ### Procedural & Advanced SQL

- [PL/pgSQL](lessons/procedural/plpgsql.md)
  - [Variables & constants](lessons/procedural/variables_constants.md)
  - [Control structures](lessons/procedural/control_structures.md)
  - [Cursors](lessons/procedural/cursors.md)
  - [Exception handling](lessons/procedural/exception_handling.md)
- [Other Procedural Languages](lessons/procedural/other_languages.md)
  - [PL/Python, PL/Perl, PL/Tcl, PL/Java](lessons/procedural/pl_other.md)
- [Triggers & Trigger Functions](lessons/procedural/triggers.md)
- [Rules](lessons/procedural/rules.md) -->

<!-- ### Security & Roles

- [Roles & Users](lessons/security/roles_users.md)
  - [Superuser vs normal user](lessons/security/superuser_vs_normal.md)
  - [Role inheritance](lessons/security/role_inheritance.md)
- [Privileges](lessons/security/privileges.md)
  - [GRANT / REVOKE](lessons/security/grant_revoke.md)
- [Row-Level Security](lessons/security/row_level_security.md)
- [Authentication Methods](lessons/security/authentication.md)
  - [Password, MD5, SCRAM](lessons/security/password_md5_scram.md)
  - [GSSAPI, SSPI](lessons/security/gssapi_sspi.md)
- [SSL / TLS](lessons/security/ssl_tls.md) -->

<!-- ### Backup & Restore

- [pg_dump / pg_restore](lessons/backup_restore/pg_dump_restore.md)
- [pg_basebackup](lessons/backup_restore/pg_basebackup.md)
- [PITR (Point-In-Time Recovery)](lessons/backup_restore/pitr.md)
- [WAL Archiving](lessons/backup_restore/wal_archiving.md) -->

<!-- ### Replication & High Availability

- [Streaming Replication](lessons/replication/streaming.md)
- [Logical Replication](lessons/replication/logical.md)
- [Physical Replication](lessons/replication/physical.md)
- [Hot Standby](lessons/replication/hot_standby.md)
- [Failover & Switchover](lessons/replication/failover_switchover.md)
- [Replication Slots](lessons/replication/slots.md) -->

<!-- ### Partitioning

- [Table Partitioning](lessons/partitioning/table_partitioning.md)
  - [Range](lessons/partitioning/range.md)
  - [List](lessons/partitioning/list.md)
  - [Hash](lessons/partitioning/hash.md)
- [Inheritance-based partitioning](lessons/partitioning/inheritance_based.md)
- [Declarative Partitioning](lessons/partitioning/declarative.md)
- [Partition Pruning](lessons/partitioning/pruning.md) -->

<!-- ### Concurrency & Locking

- [Locks](lessons/concurrency/locks.md)
  - [Row-level, Table-level, Advisory](lessons/concurrency/lock_types.md)
- [Deadlocks](lessons/concurrency/deadlocks.md)
- [MVCC internals](lessons/concurrency/mvcc_internals.md)
- [Isolation Levels](lessons/concurrency/isolation_levels.md)
  - [Read Uncommitted, Read Committed, Repeatable Read, Serializable](lessons/concurrency/isolation_types.md) -->

<!-- ### Monitoring & Maintenance

- [pg_stat views](lessons/monitoring/pg_stat_views.md)
- [Logging](lessons/monitoring/logging.md)
- [EXPLAIN / EXPLAIN ANALYZE](lessons/monitoring/explain.md)
- [VACUUM / VACUUM FULL](lessons/monitoring/vacuum.md)
- [REINDEX](lessons/monitoring/reindex.md)
- [ANALYZE](lessons/monitoring/analyze.md)
- [Auto-vacuum](lessons/monitoring/auto_vacuum.md)
- [pg_stat_statements](lessons/monitoring/pg_stat_statements.md) -->

<!-- ### Extensions & Advanced Features

- [PostGIS (Geospatial)](lessons/extensions/postgis.md)
- [Full Text Search](lessons/extensions/full_text_search.md)
- [Hstore](lessons/extensions/hstore.md)
- [Foreign Data Wrappers (FDW)](lessons/extensions/fdw.md)
- [TimescaleDB / other extensions](lessons/extensions/timescaledb.md) -->

<!-- ### Networking & Connections

- [Client-Server communication](lessons/networking/client_server.md)
- [Connection pooling](lessons/networking/connection_pooling.md)
  - [pgBouncer](lessons/networking/pgbouncer.md)
  - [pgpool-II](lessons/networking/pgpool_ii.md)
- [Listen / Notify](lessons/networking/listen_notify.md)
- [libpq & drivers](lessons/networking/libpq_drivers.md) -->

<!-- ### Miscellaneous

- [Temporary tables](lessons/misc/temporary_tables.md)
- [Unlogged tables](lessons/misc/unlogged_tables.md)
- [Inheritance](lessons/misc/inheritance.md)
- [Arrays & composite types](lessons/misc/arrays_composite.md)
- [ENUM types](lessons/misc/enum_types.md)
- [Custom types & operators](lessons/misc/custom_types_operators.md)
- [Event triggers](lessons/misc/event_triggers.md)
- [Configuration tuning](lessons/misc/config_tuning.md)
- [Logging & auditing](lessons/misc/logging_auditing.md) -->

