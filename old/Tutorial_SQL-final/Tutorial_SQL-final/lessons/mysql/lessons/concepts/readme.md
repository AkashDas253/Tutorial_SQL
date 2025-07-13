
## MySQL Concepts and Subconcepts

### Basics
- Data Definition Language (DDL)
  - CREATE, ALTER, DROP, RENAME, TRUNCATE
- Data Manipulation Language (DML)
  - SELECT, INSERT, UPDATE, DELETE
- Data Query Language (DQL)
  - SELECT
- Data Control Language (DCL)
  - GRANT, REVOKE
- Transaction Control Language (TCL)
  - COMMIT, ROLLBACK, SAVEPOINT, SET TRANSACTION

---

### Database Structure
- Database
- Schema
- Table
- Column
- Row/Record
- Data Types
  - Numeric types
  - Date and time types
  - String types
  - JSON
  - Spatial types

---

### Keys and Indexes
- Primary Key
- Foreign Key
- Unique Key
- Composite Key
- Auto Increment
- Index
  - Single-column Index
  - Composite Index
  - Full-text Index
  - Spatial Index

---

### Constraints
- NOT NULL
- UNIQUE
- DEFAULT
- CHECK
- PRIMARY KEY
- FOREIGN KEY

---

### Operators
- Arithmetic Operators
- Comparison Operators
- Logical Operators
- Bitwise Operators
- Assignment Operators

---

### Joins
- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL OUTER JOIN (emulated)
- CROSS JOIN
- SELF JOIN
- NATURAL JOIN
- USING clause
- ON clause

---

### Views and Subqueries
- CREATE VIEW
- ALTER VIEW
- DROP VIEW
- Simple subquery
- Correlated subquery
- Scalar subquery
- EXISTS / NOT EXISTS
- IN / NOT IN

---

### Functions
- Aggregate Functions
  - COUNT, SUM, AVG, MIN, MAX
- String Functions
  - CONCAT, LENGTH, REPLACE, SUBSTRING, LOWER, UPPER
- Date and Time Functions
  - NOW, CURDATE, DATE_ADD, DATEDIFF, STR_TO_DATE
- Numeric Functions
  - ROUND, CEIL, FLOOR, MOD, ABS
- Control Flow Functions
  - IF, IFNULL, CASE, COALESCE
- JSON Functions
  - JSON_OBJECT, JSON_ARRAY, JSON_EXTRACT, JSON_SET

---

### Transactions
- START TRANSACTION
- COMMIT
- ROLLBACK
- SAVEPOINT
- RELEASE SAVEPOINT
- SET AUTOCOMMIT

---

### Storage Engines
- InnoDB
- MyISAM
- MEMORY
- CSV
- ARCHIVE
- FEDERATED
- BLACKHOLE
- PERFORMANCE_SCHEMA

---

### Users and Privileges
- CREATE USER
- DROP USER
- GRANT
- REVOKE
- SET PASSWORD
- SHOW GRANTS
- Authentication Plugins
- Role Management

---

### Stored Programs
- Stored Procedures
- Stored Functions
- Triggers
  - BEFORE INSERT/UPDATE/DELETE
  - AFTER INSERT/UPDATE/DELETE
- Events
  - CREATE EVENT
  - ALTER EVENT
  - DROP EVENT
- DECLARE
- IF/ELSE
- WHILE, REPEAT, LOOP
- CURSOR

---

### Query Optimization
- EXPLAIN
- ANALYZE
- Query Cache (deprecated in newer versions)
- Index Optimization
- Table Partitioning
- Optimizer Hints

---

### Data Import/Export
- LOAD DATA INFILE
- SELECT INTO OUTFILE
- mysqldump
- mysqlimport
- mysqlpump
- Import from CSV, JSON, XML

---

### Replication
- Master-Slave Replication
- Master-Master Replication
- GTID (Global Transaction Identifiers)
- Semi-synchronous Replication
- Delayed Replication
- Multi-Source Replication

---

### Backup and Recovery
- Logical Backup
  - `mysqldump`, `mysqlpump`
- Physical Backup
  - File-level copy of data directory
- Binary Logs
- Point-in-time Recovery
- Percona XtraBackup (external tool)

---

### Security
- User Authentication
- Access Control and Privileges
- Encryption
  - Data-at-rest Encryption
  - SSL/TLS for data-in-transit
- SQL Injection Protection
- Firewall Plugin (Enterprise)

---

### Monitoring and Performance
- SHOW STATUS
- SHOW PROCESSLIST
- INFORMATION_SCHEMA
- PERFORMANCE_SCHEMA
- Slow Query Log
- General Log
- Error Log

---

### System Administration
- Configuration (`my.cnf`, `my.ini`)
- Server Startup and Shutdown
- User Management
- Log Files
- Time Zone Settings
- Resource Limits
- Environment Variables

---

### Tools and Interfaces
- MySQL CLI
- MySQL Workbench
- phpMyAdmin
- MySQL Shell
- MySQL Router
- MySQL Utilities (deprecated)

---
