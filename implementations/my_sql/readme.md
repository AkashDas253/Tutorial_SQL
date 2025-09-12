## MySQL

### Notes specific
- [Overview](lessons/overview/readme.md)
- [Concepts](lessons/concepts/readme.md)
- [Documentation](https://dev.mysql.com/doc/)

---

### SQL Part

#### Language Types
- [Data Definition Language (DDL)](lessons/languages/ddl.md)
- [Data Manipulation Language (DML)](lessons/languages/dml.md)  
- [Data Query Language (DQL)](lessons/languages/dql.md)  
- [Data Control Language (DCL)](lessons/languages/dcl.md)  
- [Transaction Control Language (TCL)](lessons/languages/tcl.md)

#### Database Structure
- [Database Structure](lessons/database_structure/readme.md)
<!-- [Database](lessons/database_structure/database/readme.md)  
- [Schema](lessons/database_structure/schema/readme.md)  
- [Table](lessons/database_structure/table/readme.md)  
- [Column](lessons/database_structure/column/readme.md)  
- [Row/Record](lessons/database_structure/row_record/readme.md)  -->

#### Data Types
- [Data Types](lessons/data_types/readme.md)  
- [Numeric types](lessons/data_types/numeric_types/readme.md)  
- [Date and Time types](lessons/data_types/date_time_types/readme.md)  
- [String types](lessons/data_types/string_types/readme.md)  
- [JSON](lessons/data_types/json/readme.md)  
- [Spatial types](lessons/data_types/spatial_types/readme.md)

#### Key
- [Keys](lessons/keys/readme.md)
<!-- - [Primary Key](lessons/keys_indexes/primary_key/readme.md)  
- [Foreign Key](lessons/keys_indexes/foreign_key/readme.md)  
- [Unique Key](lessons/keys_indexes/unique_key/readme.md)  
- [Composite Key](lessons/keys_indexes/composite_key/readme.md)  
- [Auto Increment](lessons/keys_indexes/auto_increment/readme.md)   -->

#### Index
- [Index](lessons/index/readme.md)  
- [Single-column Index](lessons/indexes/single_column_index.md)  
<!-- - [Composite Index](lessons/indexes/composite_index/readme.md)  
- [Full-text Index](lessons/indexes/full_text_index/readme.md)  
- [Spatial Index](lessons/indexes/spatial_index/readme.md) -->

#### Constraints
- [Constraints](lessons/constraints/readme.md) 
- [NOT NULL](lessons/constraints/not_null.md)  
- [UNIQUE](lessons/constraints/unique.md)  
- [DEFAULT](lessons/constraints/default.md)  
- [CHECK](lessons/constraints/check.md)  
- [PRIMARY KEY](lessons/constraints/primary_key.md)  
- [FOREIGN KEY](lessons/constraints/foreign_key.md)

#### Views and Subqueries and others
- [Views](lessons/views/readme.md) 
- [CREATE VIEW](lessons/views/create_view.md)  
- [ALTER VIEW](lessons/views/alter_view.md)  
- [DROP VIEW](lessons/views/drop_view.md)  

#### Subqueries
- [Subqueries](lessons/subqueries/readme.md)
- [Simple subquery](lessons/subqueries/simple_subquery.md)  
- [Correlated subquery](lessons/subqueries/correlated_subquery.md)  
- [Scalar subquery](lessons/subqueries/scalar_subquery.md)  
- [EXISTS / NOT EXISTS](lessons/subqueries/exists_not_exists.md)  
- [IN / NOT IN](lessons/subqueries/in_not_in.md)

#### CTE
- [CTE](lessons/cte/cte.md)
- [Recursive CTE](lessons/cte/recursive_cte.md)

#### Operators
- [Operators](lessons/operators/readme.md)  
<!-- - [Arithmetic Operators](lessons/operators/arithmetic_operators/readme.md)  
- [Comparison Operators](lessons/operators/comparison_operators/readme.md)  
- [Logical Operators](lessons/operators/logical_operators/readme.md)  
- [Bitwise Operators](lessons/operators/bitwise_operators/readme.md)  
- [Assignment Operators](lessons/operators/assignment_operators/readme.md) -->

#### Joins
- [Joins](lessons/joins/readme.md)
<!-- - [INNER JOIN](lessons/joins/inner_join/readme.md)  
- [LEFT JOIN](lessons/joins/left_join/readme.md)  
- [RIGHT JOIN](lessons/joins/right_join/readme.md)  
- [FULL OUTER JOIN](lessons/joins/full_outer_join/readme.md)  
- [CROSS JOIN](lessons/joins/cross_join/readme.md)  
- [SELF JOIN](lessons/joins/self_join/readme.md)  
- [NATURAL JOIN](lessons/joins/natural_join/readme.md)  
- [USING clause](lessons/joins/using_clause/readme.md)  
- [ON clause](lessons/joins/on_clause/readme.md) -->

#### Functions
- [Aggregate Functions](lessons/functions/aggregate_functions/readme.md)
- [Window Function](lessons/functions/window_functions/readme.md): [Functions Reference](lessons/functions/window_functions/functionreference.md)
  <!-- - [COUNT](lessons/functions/aggregate_functions/count/readme.md), [SUM](lessons/functions/aggregate_functions/sum/readme.md), [AVG](lessons/functions/aggregate_functions/avg/readme.md), [MIN](lessons/functions/aggregate_functions/min/readme.md), [MAX](lessons/functions/aggregate_functions/max/readme.md) -->
- [String Functions](lessons/functions/string_functions/readme.md)
  <!-- - [CONCAT](lessons/functions/string_functions/concat/readme.md), [LENGTH](lessons/functions/string_functions/length/readme.md), [REPLACE](lessons/functions/string_functions/replace/readme.md), [SUBSTRING](lessons/functions/string_functions/substring/readme.md), [LOWER](lessons/functions/string_functions/lower/readme.md), [UPPER](lessons/functions/string_functions/upper/readme.md) -->
- [Date and Time Functions](lessons/functions/date_time_functions/readme.md)
  <!-- - [NOW](lessons/functions/date_time_functions/now/readme.md), [CURDATE](lessons/functions/date_time_functions/curdate/readme.md), [DATE_ADD](lessons/functions/date_time_functions/date_add/readme.md), [DATEDIFF](lessons/functions/date_time_functions/datediff/readme.md), [STR_TO_DATE](lessons/functions/date_time_functions/str_to_date/readme.md) -->
- [Numeric Functions](lessons/functions/numeric_functions/readme.md)
  <!-- - [ROUND](lessons/functions/numeric_functions/round/readme.md), [CEIL](lessons/functions/numeric_functions/ceil/readme.md), [FLOOR](lessons/functions/numeric_functions/floor/readme.md), [MOD](lessons/functions/numeric_functions/mod/readme.md), [ABS](lessons/functions/numeric_functions/abs/readme.md) -->
- [Control Flow Functions](lessons/functions/control_flow_functions/readme.md)
  <!-- - [IF](lessons/functions/control_flow_functions/if/readme.md), [IFNULL](lessons/functions/control_flow_functions/ifnull/readme.md), [CASE](lessons/functions/control_flow_functions/case/readme.md), [COALESCE](lessons/functions/control_flow_functions/coalesce/readme.md) -->
- [JSON Functions](lessons/functions/json_functions/readme.md)
  <!-- - [JSON_OBJECT](lessons/functions/json_functions/json_object/readme.md), [JSON_ARRAY](lessons/functions/json_functions/json_array/readme.md), [JSON_EXTRACT](lessons/functions/json_functions/json_extract/readme.md), [JSON_SET](lessons/functions/json_functions/json_set/readme.md) -->

---

### Administration

#### Transactions
- [Transactions](lessons/transactions/readme.md)
<!-- - [START TRANSACTION](lessons/transactions/start_transaction/readme.md)
- [COMMIT](lessons/transactions/commit/readme.md)
- [ROLLBACK](lessons/transactions/rollback/readme.md)
- [SAVEPOINT](lessons/transactions/savepoint/readme.md)
- [RELEASE SAVEPOINT](lessons/transactions/release_savepoint/readme.md)
- [SET AUTOCOMMIT](lessons/transactions/set_autocommit/readme.md) -->


#### Users and Privileges
- [Users and Privileges](lessons/users_privileges/readme.md)
<!-- - [CREATE USER](lessons/users_privileges/create_user/readme.md)
- [DROP USER](lessons/users_privileges/drop_user/readme.md)
- [GRANT](lessons/users_privileges/grant/readme.md)
- [REVOKE](lessons/users_privileges/revoke/readme.md)
- [SET PASSWORD](lessons/users_privileges/set_password/readme.md)
- [SHOW GRANTS](lessons/users_privileges/show_grants/readme.md)
- [Authentication Plugins](lessons/users_privileges/authentication_plugins/readme.md)
- [Role Management](lessons/users_privileges/role_management/readme.md) -->

---

### Stored Program
- [Stored Procedures](lessons/stored_procedures/readme.md)
- [Stored Functions](lessons/stored_functions/readme.md)
- [Triggers](lessons/triggers/readme.md)
  <!-- - [BEFORE INSERT/UPDATE/DELETE](lessons/triggers/before/readme.md)
  - [AFTER INSERT/UPDATE/DELETE](lessons/triggers/after/readme.md) -->
- [Events](lessons/events/readme.md)
  <!-- - [CREATE EVENT](lessons/events/create_event/readme.md)
  - [ALTER EVENT](lessons/events/alter_event/readme.md)
  - [DROP EVENT](lessons/events/drop_event/readme.md) -->
- [DECLARE](lessons/declare/readme.md)
- [IF/ELSE](lessons/if_else/readme.md)
- [WHILE, REPEAT, LOOP](lessons/loops/readme.md)
- [CURSOR](lessons/cursor/readme.md)

---

### Query Optimization
- [Query Optimization](lessons/query_optimization/readme.md)
- [EXPLAIN](lessons/explain/readme.md)
- [ANALYZE](lessons/analyze/readme.md)
- [Query Cache](lessons/query_cache/readme.md) (deprecated in newer versions)
- [Index Optimization](lessons/index_optimization/readme.md)
- [Table Partitioning](lessons/table_partitioning/readme.md)
- [Optimizer Hints](lessons/optimizer_hints/readme.md)

---

### Replication
- [Replication](lessons/replication/readme.md)
<!-- - [Master-Slave Replication](lessons/master_slave_replication/readme.md)
- [Master-Master Replication](lessons/master_master_replication/readme.md)
- [GTID (Global Transaction Identifiers)](lessons/gtid/readme.md)
- [Semi-synchronous Replication](lessons/semi_synchronous_replication/readme.md)
- [Delayed Replication](lessons/delayed_replication/readme.md)
- [Multi-Source Replication](lessons/multi_source_replication/readme.md) -->

### Backup and Recovery
- [Backup and Recovery](lessons/backup_recovery/readme.md)
<!-- - [Logical Backup](lessons/logical_backup/readme.md)
  - [`mysqldump`, `mysqlpump`](lessons/mysqldump_mysqlpump/readme.md)
- [Physical Backup](lessons/physical_backup/readme.md)
  - [File-level copy of data directory](lessons/file_level_copy/readme.md)
- [Binary Logs](lessons/binary_logs/readme.md)
- [Point-in-time Recovery](lessons/point_in_time_recovery/readme.md)
- [Percona XtraBackup (external tool)](lessons/percona_xtrabackup/readme.md) -->

### Security
- [Security](lessons/security/readme.md)
<!-- - [User Authentication](lessons/user_authentication/readme.md)
- [Access Control and Privileges](lessons/access_control_privileges/readme.md)
- [Encryption](lessons/encryption/readme.md)
  - [Data-at-rest Encryption](lessons/data_at_rest_encryption/readme.md)
  - [SSL/TLS for data-in-transit](lessons/ssl_tls_data_in_transit/readme.md)
- [SQL Injection Protection](lessons/sql_injection_protection/readme.md)
- [Firewall Plugin (Enterprise)](lessons/firewall_plugin/readme.md) -->

### Monitoring and Performance
- [Monitoring and Performance](lessons/monitoring_performance/readme.md)
<!-- - [SHOW STATUS](lessons/show_status/readme.md)
- [SHOW PROCESSLIST](lessons/show_processlist/readme.md)
- [INFORMATION_SCHEMA](lessons/information_schema/readme.md)
- [PERFORMANCE_SCHEMA](lessons/performance_schema/readme.md)
- [Slow Query Log](lessons/slow_query_log/readme.md)
- [General Log](lessons/general_log/readme.md)
- [Error Log](lessons/error_log/readme.md) -->

### System Administration
- [System Administration](lessons/system_administration/readme.md)
<!-- - [Configuration (`my.cnf`, `my.ini`)](lessons/configuration/readme.md)
- [Server Startup and Shutdown](lessons/server_startup_shutdown/readme.md)
- [User Management](lessons/user_management/readme.md)
- [Log Files](lessons/log_files/readme.md)
- [Time Zone Settings](lessons/time_zone_settings/readme.md)
- [Resource Limits](lessons/resource_limits/readme.md)
- [Environment Variables](lessons/environment_variables/readme.md) -->

### Storage Engines
- [Storage Engines](lessons/storage_engines/readme.md)
<!-- - [InnoDB](lessons/storage_engines/innodb/readme.md)
- [MyISAM](lessons/storage_engines/myisam/readme.md)
- [MEMORY](lessons/storage_engines/memory/readme.md)
- [CSV](lessons/storage_engines/csv/readme.md)
- [ARCHIVE](lessons/storage_engines/archive/readme.md)
- [FEDERATED](lessons/storage_engines/federated/readme.md)
- [BLACKHOLE](lessons/storage_engines/blackhole/readme.md)
- [PERFORMANCE_SCHEMA](lessons/storage_engines/performance_schema/readme.md) -->

---

### Tools and Interfaces
- [Tools and Interfaces](lessons/tools_and_interfaces/readme.md)
<!-- - [MySQL CLI](lessons/mysql_cli/readme.md)
- [MySQL Workbench](lessons/mysql_workbench/readme.md)
- [phpMyAdmin](lessons/phpmyadmin/readme.md)
- [MySQL Shell](lessons/mysql_shell/readme.md)
- [MySQL Router](lessons/mysql_router/readme.md)
- [MySQL Utilities (deprecated)](lessons/mysql_utilities/readme.md) -->

---

### Data Import/Export
- [Data Import/Export](lessons/data_import_export/readme.md)
<!-- - [LOAD DATA INFILE](lessons/data_import_export/load_data_infile/readme.md)
- [SELECT INTO OUTFILE](lessons/data_import_export/select_into_outfile/readme.md)
- [mysqldump](lessons/data_import_export/mysqldump/readme.md)
- [mysqlimport](lessons/data_import_export/mysqlimport/readme.md)
- [mysqlpump](lessons/data_import_export/mysqlpump/readme.md)
- [Import from CSV, JSON, XML](lessons/data_import_export/import_formats/readme.md) -->

---