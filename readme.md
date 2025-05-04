# SQL Notes

## Combined

---

- [Cheatsheet](lessons/cheatsheet/readme.md)
- [Basics](lessons/basics/readme.md)
- [Concepts](lessons/concepts/readme.md) 

- [Types of SQL](lessons/types_of_SQL/readme.md)

    - [Data Definition Language (DDL)](lessons/ddl/readme.md)

    - [Data Manipulation Language (DML)](lessons/dml/readme.md)
        - [Database Specific Implementation](lessons/dml_database_specific/readme.md)

    - [Transaction Control Language (TCL)](lessons/tcl/readme.md)
        - [Nested and Distributed Transaction](lessons/nested_distributed_transaction/readme.md)

    - [Data Control Language (DCL)](lessons/dcl/readme.md)
      - [Multi-role management](lessons/dcl_multi_role_management/readme.md)
      - [Permission inheritance](lessons/permission_inheritance/readme.md)

    - [Data Query Language (DQL)](lessons/dql/readme.md)



- [Query and Schema Constraints](lessons/constraints/readme.md)



- [Procedural SQL (PL/SQL or T-SQL)](lessons/procedural_sql/readme.md)



- [SQL Data Types](lessons/datatypes/readme.md)

    - [Database Compatibility](lessons/datatypes_compatibility/readme.md)
        - [Oracle SQL Datatypes](lessons/datatypes_oracle/oracle_sql/readme.md)

    - [Advanced Usage](lessons/datatypes_usage/readme.md)



- [SQL Operators](lessons/operator/readme.md)



- Function:
    - [Aggregate Functions](lessons/aggregate/readme.md)
    - [Mathematical Functions](lessons/mathematical_functions/readme.md)
    - [Null Value Functions](lessons/null_value_functions/readme.md)
    - [Window](lessons/window/readme.md)
    - [String Functions](lessons/string_functions/readme.md)
    - [Date and Time Functions](lessons/date_time_functions/readme.md)
    - [Conversion Functions](lessons/conversion_functions/readme.md)
    - [Conditional Functions](lessons/conditional_functions/readme.md)



- Advanced SQL Features
  - [Views](lessons/views/readme.md)

  - [Indexes](lessons/index/readme.md)

  - [Partitioning](lessons/partiontioning/readme.md) 


<!-- 
### 10. Extensions and Vendor-Specific Features
- MySQL:  
  - AUTO_INCREMENT  
  - ENGINE Types (InnoDB, MyISAM)  
  - Full-Text Search  
- PostgreSQL:  
  - Table Inheritance  
  - Rich JSON Support (JSONB)  
  - Lateral Joins  
- Oracle SQL:  
  - Hierarchical Queries (CONNECT BY)  
  - Flashback Queries  
  - PL/SQL Packages  
- SQL Server:  
  - WITH (NOLOCK)  
  - Computed Columns  
  - Columnstore Indexes  

---

### 11. Database Administration
- Backup and Recovery  
- User Management  
  - CREATE USER  
  - ALTER USER  
  - DROP USER  
- Database Management
  - CREATE DATABASE  
  - ALTER DATABASE  
  - DROP DATABASE  

---

### 12. Performance Optimization
- Query Optimization  
- Execution Plans  
- Hints  
  - Optimizer Hints (Oracle SQL, SQL Server)  

---

### 13. Analytical and Aggregate Functions
- ROW_NUMBER(), RANK(), DENSE_RANK()  
- LEAD(), LAG()  
- NTILE()  
- PERCENTILE_CONT, PERCENTILE_DISC (PostgreSQL, SQL Server)  

---

### 14. Security Features
- Role Management  
- Encryption (SQL Server TDE, Oracle Advanced Security)  
- Row-Level Security (SQL Server, PostgreSQL)  

--- 

### 15. NoSQL Extensions in SQL Databases
- JSON/Document Handling (PostgreSQL, MySQL, SQL Server)  
- Key-Value Data Stores  
 -->

---


## Implementation wise

---

### [ANSI SQL](lessons/ansi_sql/ansi_sql/readme.md)

- [ANSI Data Definition Language (DDL)](lessons/ansi_sql/ansi_ddl/readme.md) 
- [ANSI Data Manipulation Language (DML)](lessons/ansi_sql/ansi_dml/readme.md) 
- [ANSI Data Query Language (DQL)](lessons/ansi_sql/ansi_dql/readme.md)
- [ANSI Data Control Language (DCL)](lessons/ansi_sql/ansi_dcl/readme.md)  
- [ANSI Transaction Control Language (TCL)](lessons/ansi_sql/ansi_tcl/readme.md)  
- [ANSI Datatypes](lessons/ansi_sql/ansi_data_types/readme.md) 
- [ANSI Constraints](lessons/ansi_sql/ansi_constraints/readme.md)  
- [ANSI Joins](lessons/ansi_sql/ansi_joins/readme.md) 
- [ANSI Subqueries](lessons/ansi_sql/ansi_subqueries/readme.md) 
- [ANSI SQL Operators](lessons/ansi_sql/ansi_sql_operators/readme.md) 
- [ANSI SQL Functions](lessons/ansi_sql/ansi_sql_functions/readme.md) 
- [ANSI Indexing](lessons/ansi_sql/ansi_indexing/readme.md) 
- [ANSI Views](lessons/ansi_sql/ansi_views/readme.md) 

---

### [Oracle SQL](lessons/oracle_sql/oracle_sql/readme.md)

- [Oracle Syntax](lessons/oracle_sql/oracle_syntax/readme.md) 
- [Oracle Datatypes](lessons/oracle_sql/oracle_datatype/readme.md) 
- [Oracle Operators](lessons/oracle_sql/oracle_operator/readme.md)   
- [Oracle Database Objects](lessons/oracle_sql/oracle_objects/readme.md) 
- [Oracle Data Manipulation Language (DML)](lessons/oracle_sql/oracle_dml/readme.md) 
- [Oracle Data Definition Language (DDL)](lessons/oracle_sql/oracle_ddl/readme.md) 
- [Oracle Data Query Language (DQL)](lessons/oracle_sql/oracle_dql/readme.md) 
- [Oracle Data Control Language (DCL)](lessons/oracle_sql/oracle_dcl/readme.md) 
- [Oracle Transaction Control Language (TCL)](lessons/oracle_sql/oracle_tcl/readme.md) 
- [Oracle Query Features](lessons/oracle_sql/oracle_query_features/readme.md) 
- [Oracle Advanced Features](lessons/oracle_sql/oracle_advanced_features/readme.md)   
- [Oracle Security and Management](lessons/oracle_sql/oracle_security_and_management/readme.md)  
- [Oracle Performance Optimization](lessons/oracle_sql/oracle_performance_optimization/readme.md)  
- [Oracle Backup and Recovery](lessons/oracle_sql/oracle_backup_and_recovery/readme.md) 

---

### [PL/SQL](lessons/pl_sql/plsql/readme.md) 

- [PL/SQL Architecture](lessons/pl_sql/plsql_architecture/readme.md) 
- [PL/SQL Block Structure](lessons/pl_sql/plsql_block_structure/readme.md) 
- [Data Types in PL/SQL](lessons/pl_sql/plsql_data_types/readme.md)  
- [Control Structures](lessons/pl_sql/plsql_control_structures/readme.md) 
- [Cursors](lessons/pl_sql/plsql_cursors/readme.md) 
- [Triggers](lessons/pl_sql/plsql_triggers/readme.md) 
- [Procedures and Functions](lessons/pl_sql/plsql_procedures_functions/readme.md) 
- [Packages](lessons/pl_sql/plsql_packages/readme.md)  
- [Exception Handling](lessons/pl_sql/plsql_exception_handling/readme.md)
- [PL/SQL Collections](lessons/pl_sql/plsql_collections/readme.md)  
- [Dynamic SQL](lessons/pl_sql/plsql_dynamic_sql/readme.md) 
- [Built-in Functions](lessons/pl_sql/plsql_built_in_functions/readme.md) 
- [Transactions in PL/SQL](lessons/pl_sql/plsql_transactions/readme.md) 
- [Advanced Concepts](lessons/pl_sql/plsql_advanced_concepts/readme.md) 
- [Security in PL/SQL](lessons/pl_sql/plsql_security/readme.md)
- [PL/SQL Optimization](lessons/pl_sql/plsql_optimization/readme.md) 

---

### [Posgres SQL](lessons/posgres_sql/readme.md)

- [Syntax](lessons/postgres_syntax/readme.dm)
- [Installation & Setup Cheatsheet](lessons/postgres_cheatsheet_installation_setup/readme.md)  
- [Database Structure](lessons/postgres_database_structure/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_database_structure/readme.md)  
- [SQL Statements Cheatsheet](lessons/postgres_cheatsheet_sql_statements/readme.md)  
    - [Data Definition Language (DDL)](lessons/postgres_ddl/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_ddl/readme.md)  
    - [Data Manipulation Language (DML)](lessons/postgres_dml/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_dml/readme.md)  
    - [Data Query Language (DQL)](lessons/postgres_dql/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_dql/readme.md)  
    - [Data Control Language (DCL)](lessons/postgres_dcl/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_dcl/readme.md)  
    - [Transaction Control Language (TCL)](lessons/postgres_tcl/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_tcl/readme.md)  

---

- [Data Types](lessons/postgres_data_types/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_data_types/readme.md)  
    - [Numeric](lessons/postgres_numeric_data_type/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_numeric_data_type/readme.md)  
    - [Character](lessons/postgres_character_data_type/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_character_data_type/readme.md)  
    - [Date & Time](lessons/postgres_date_time_data_type/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_date_time_data_type/readme.md)  
    - [Boolean](lessons/postgres_boolean_data_type/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_boolean_data_type/readme.md)  
    - [JSON/JSONB](lessons/postgres_json_jsonb_data_type/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_json_jsonb_data_type/readme.md)  
    - [Array](lessons/postgres_array_data_type/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_array_data_type/readme.md)  
- [Operators](lessons/postgres_operator/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_operator/readme.md)  
- [Constraints](lessons/postgres_constraints/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_constraints/readme.md)  
- [Indexing](lessons/postgres_indexing/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_indexing/readme.md)  
- [Joins](lessons/postgres_joins/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_joins/readme.md)  
- [Views](lessons/postgres_views/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_views/readme.md)  
- [Materialized Views](lessons/postgres_materialized_views/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_materialized_views/readme.md)  
- [Transactions](lessons/postgres_transactions/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_transactions/readme.md)  

---

- [Functions & Procedures](lessons/postgres_functions_procedures/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_functions_procedures/readme.md)  
- [Functions](lessons/postgres_functions/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_functions/readme.md)  
- [Procedures](lessons/postgres_procedures/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_procedures/readme.md)  
- [Triggers](lessons/postgres_triggers/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_triggers/readme.md)  
- [Query Optimization](lessons/postgres_query_optimization/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_query_optimization/readme.md)  
- [JSON Support](lessons/postgres_json/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_json/readme.md)  
- [XML Support](lessons/postgres_xml/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_xml/readme.md)  
- [Full-Text Search](lessons/postgres_full_text_search/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_full_text_search/readme.md)  
- [Security](lessons/postgres_security/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_security/readme.md)  
- [High Availability & Replication](lessons/postgres_replication/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_replication/readme.md)  
- [Partitioning](lessons/postgres_partitioning/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_partitioning/readme.md)  
- [Inheritance](lessons/postgres_inheritance/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_inheritance/readme.md)  
- [Parallel Query Execution](lessons/postgres_parallel_query/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_parallel_query/readme.md)  
- [Window Functions](lessons/postgres_window_functions/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_window_functions/readme.md)  
- [Common Table Expressions (CTEs)](lessons/postgres_cte/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_cte/readme.md)  
- [Foreign Data Wrappers (FDW)](lessons/postgres_fdw/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_fdw/readme.md)  
- [Event Triggers](lessons/postgres_event_triggers/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_event_triggers/readme.md)  
- [Backup & Recovery](lessons/postgres_backup_recovery/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_backup_recovery/readme.md)  
- [Performance Monitoring](lessons/postgres_performance_monitoring/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_performance_monitoring/readme.md)  
- [Geospatial Data](lessons/postgres_geospatial/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_geospatial/readme.md)  
- [Time-Series Data](lessons/postgres_time_series/readme.md) - [Cheatsheet](lessons/postgres_cheatsheet_time_series/readme.md)  

---

<!-- 
### [Posgres SQL](lessons/posgres_sql/readme.md)

### [Basic Concepts](lessons/posgres_sql_basic_concepts/readme.md)

- [Data Types](lessons/posgres_sql_data_types/readme.md)
- [SQL Syntax](lessons/posgres_sql_sql_syntax/readme.md)
- [Identifiers and Literals](lessons/posgres_sql_identifiers_literals/readme.md)

### [Database Management](lessons/posgres_sql_database_management/readme.md)

- [Database Creation](lessons/posgres_sql_database_creation/readme.md)
- [Schemas](lessons/posgres_sql_schemas/readme.md)
- [Roles and Permissions](lessons/posgres_sql_roles_permissions/readme.md)
- [Backup and Restore](lessons/posgres_sql_backup_restore/readme.md)
- [Monitoring and Logs](lessons/posgres_sql_monitoring_logs/readme.md)

### [Table Management](lessons/posgres_sql_table_management/readme.md)

- [Table Types](lessons/posgres_sql_table_types/readme.md)
- [Table Operations](lessons/posgres_sql_table_operations/readme.md)
- [Constraints](lessons/posgres_sql_constraints/readme.md)
- [Indexes](lessons/posgres_sql_indexes/readme.md)

### [Query Optimization](lessons/posgres_sql_query_optimization/readme.md)

- [Query Plans](lessons/posgres_sql_query_plans/readme.md)
- [Vacuum and Analyze](lessons/posgres_sql_vacuum_analyze/readme.md)
- [Partitioning](lessons/posgres_sql_partitioning/readme.md)
- [Clustering](lessons/posgres_sql_clustering/readme.md)

### [Advanced Features](lessons/posgres_sql_advanced_features/readme.md)

- [Triggers](lessons/posgres_sql_triggers/readme.md)
- [Stored Procedures](lessons/posgres_sql_stored_procedures/readme.md)
- [Views](lessons/posgres_sql_views/readme.md)
- [Foreign Data Wrappers (FDW)](lessons/posgres_sql_fdw/readme.md)

### [Transactions](lessons/posgres_sql_transactions/readme.md)

- [Transaction Control](lessons/posgres_sql_transaction_control/readme.md)
- [Isolation Levels](lessons/posgres_sql_isolation_levels/readme.md)
- [Savepoints](lessons/posgres_sql_savepoints/readme.md)

### [Extensions](lessons/posgres_sql_extensions/readme.md)

- [Common Extensions](lessons/posgres_sql_common_extensions/readme.md)
- [Management](lessons/posgres_sql_extension_management/readme.md)

### [JSON and JSONB](lessons/posgres_sql_json_jsonb/readme.md)

- [JSON Operations](lessons/posgres_sql_json_operations/readme.md)
- [Querying JSON](lessons/posgres_sql_querying_json/readme.md)

### [Security](lessons/posgres_sql_security/readme.md)

- [Authentication](lessons/posgres_sql_authentication/readme.md)
- [SSL and Encryption](lessons/posgres_sql_ssl_encryption/readme.md)
- [Row-Level Security](lessons/posgres_sql_row_level_security/readme.md)

### [Replication and High Availability](lessons/posgres_sql_replication_high_availability/readme.md)

- [Replication Types](lessons/posgres_sql_replication_types/readme.md)
- [Clustering](lessons/posgres_sql_clustering/readme.md)
- [Tools](lessons/posgres_sql_tools/readme.md)

### [Performance Tuning](lessons/posgres_sql_performance_tuning/readme.md)

- [Configuration](lessons/posgres_sql_configuration/readme.md)
- [Caching](lessons/posgres_sql_caching/readme.md)
- [Connection Pooling](lessons/posgres_sql_connection_pooling/readme.md)

### [Miscellaneous](lessons/posgres_sql_miscellaneous/readme.md)

- [Foreign Keys and Relationships](lessons/posgres_sql_foreign_keys_relationships/readme.md)
- [Inheritance](lessons/posgres_sql_inheritance/readme.md)
- [Time Zone Support](lessons/posgres_sql_time_zone_support/readme.md)
- [Event Triggers](lessons/posgres_sql_event_triggers/readme.md) -->

### [MySQL](lessons/mysql/readme.md)