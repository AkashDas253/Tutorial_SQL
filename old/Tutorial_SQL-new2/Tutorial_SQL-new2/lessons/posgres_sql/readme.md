## Posgres SQL cheatsheet

- PostgreSQL Basics  
  - Installation & Setup  
  - Database Structure  
  - Data Types  

- SQL Statements  
  - DDL (CREATE, ALTER, DROP)  
  - DML (INSERT, UPDATE, DELETE)  
  - DQL (SELECT)  
  - DCL (GRANT, REVOKE)  
  - TCL (COMMIT, ROLLBACK, SAVEPOINT)  

- Data Types  
  - Numeric  
  - Character  
  - Date & Time  
  - Boolean  
  - JSON/JSONB  
  - Arrays  

- Constraints  
  - Primary Key  
  - Foreign Key  
  - Unique  
  - Check  
  - Not Null  

- Indexing  
  - B-Tree Index  
  - Hash Index  
  - GIN & GiST Index  
  - Partial Indexes  

- Joins  
  - INNER JOIN  
  - LEFT JOIN  
  - RIGHT JOIN  
  - FULL JOIN  
  - CROSS JOIN  

- Views & Materialized Views  
  - Creating Views  
  - Updating Views  
  - Refreshing Materialized Views  

- Transactions  
  - ACID Properties  
  - Savepoints  
  - Isolation Levels  

- Functions & Procedures  
  - PL/pgSQL  
  - User-Defined Functions  
  - Stored Procedures  

- Triggers  
  - BEFORE & AFTER Triggers  
  - Row-Level & Statement-Level Triggers  

- Query Optimization  
  - EXPLAIN & EXPLAIN ANALYZE  
  - Vacuum & Analyze  
  - Query Caching  

- JSON & XML Support  
  - JSONB vs JSON  
  - Querying JSON Data  
  - XML Functions  

- Full-Text Search  
  - `tsvector` & `tsquery`  
  - Indexing for Full-Text Search  

- Security  
  - Role Management  
  - Authentication Methods  
  - SSL Configuration  

- High Availability & Replication  
  - Streaming Replication  
  - Logical Replication  
  - Connection Pooling  

- **Partitioning**  
  - Range Partitioning  
  - List Partitioning  
  - Hash Partitioning  

- **Inheritance**  
  - Table Inheritance  
  - Querying Parent & Child Tables  

- **Parallel Query Execution**  
  - Parallel Sequential Scans  
  - Parallel Joins  
  - Parallel Aggregations  

- **Window Functions**  
  - Ranking (`ROW_NUMBER`, `RANK`, `DENSE_RANK`)  
  - Aggregate Functions (`SUM() OVER`, `AVG() OVER`)  
  - Moving Averages  

- **Common Table Expressions (CTEs)**  
  - Recursive CTEs  
  - Non-Recursive CTEs  

- **Logical & Bitwise Operators**  
  - Boolean Operators (`AND`, `OR`, `NOT`)  
  - Bitwise Operators (`&`, `|`, `^`, `<<`, `>>`)  

- **Foreign Data Wrappers (FDW)**  
  - PostgreSQL FDW  
  - Connecting to External Databases  

- **Event Triggers**  
  - DDL Triggers  
  - Auditing Schema Changes  

- **Backup & Recovery**  
  - `pg_dump`  
  - `pg_restore`  
  - PITR (Point-In-Time Recovery)  

- **Performance Monitoring**  
  - `pg_stat_statements`  
  - `pg_stat_activity`  
  - `pg_buffercache`  

- **JSON Processing**  
  - `jsonb` Operators & Functions  
  - Indexing JSON Data  

- **Geospatial Data**  
  - PostGIS Extension  
  - Geometric Data Types  

- **Time-Series Data**  
  - `timescaledb` Extension  
  - Continuous Aggregates  

---

## **PostgreSQL Concepts and Subconcepts**

### **1. Basic Concepts**
- **Data Types**
  - Numeric types (e.g., `INTEGER`, `DECIMAL`, `SERIAL`)
  - Character types (e.g., `CHAR`, `VARCHAR`, `TEXT`)
  - Date/time types (e.g., `DATE`, `TIME`, `TIMESTAMP`)
  - Boolean type (`BOOLEAN`)
  - Geometric types (e.g., `POINT`, `LINE`, `POLYGON`)
  - JSON/JSONB types
  - Arrays
  - Enumerated types (Enums)
  - UUID

- **SQL Syntax**
  - `SELECT`, `INSERT`, `UPDATE`, `DELETE`
  - WHERE clause
  - JOIN types (`INNER`, `OUTER`, `CROSS`)
  - Subqueries
  - CASE expressions
  - Common Table Expressions (CTEs)

- **Identifiers and Literals**
  - Quoted identifiers
  - Case sensitivity

---

### **2. Database Management**
- **Database Creation**
  - `CREATE DATABASE`
  - Connection management (`\c`, `pgAdmin`, etc.)

- **Schemas**
  - Public schema
  - Custom schema creation (`CREATE SCHEMA`)
  - Schema search path

- **Roles and Permissions**
  - Role creation and assignment (`CREATE ROLE`)
  - GRANT and REVOKE statements
  - Superuser roles

- **Backup and Restore**
  - `pg_dump` for backup
  - `pg_restore` for restore
  - Logical vs. physical backups

- **Monitoring and Logs**
  - `pg_stat_activity`
  - Server logs
  - `EXPLAIN` and `ANALYZE`

---

### **3. Table Management**
- **Table Types**
  - Permanent tables
  - Temporary tables
  - Unlogged tables

- **Table Operations**
  - Create: `CREATE TABLE`
  - Alter: `ALTER TABLE` (e.g., add column, modify type)
  - Drop: `DROP TABLE`

- **Constraints**
  - Primary key
  - Foreign key
  - Unique
  - Check
  - Not null

- **Indexes**
  - B-tree indexes
  - GIN and GiST indexes
  - BRIN indexes
  - `CREATE INDEX`
  - Partial indexes
  - Covering indexes

---

### **4. Query Optimization**
- **Query Plans**
  - `EXPLAIN` for execution plan
  - Index usage
  - Cost estimation

- **Vacuum and Analyze**
  - Autovacuum
  - `VACUUM` for reclaiming storage
  - `ANALYZE` for statistics updates

- **Partitioning**
  - Declarative partitioning
  - Inheritance-based partitioning
  - Subpartitioning

- **Clustering**
  - `CLUSTER` command
  - Table reorganization

---

### **5. Advanced Features**
- **Triggers**
  - `BEFORE`, `AFTER`, `INSTEAD OF` triggers
  - `CREATE TRIGGER`

- **Stored Procedures**
  - `PL/pgSQL`
  - Procedure creation (`CREATE PROCEDURE`)
  - Function creation (`CREATE FUNCTION`)
  - Procedural languages support (`PLPython`, `PLPerl`)

- **Views**
  - Simple views
  - Materialized views
  - `REFRESH MATERIALIZED VIEW`

- **Foreign Data Wrappers (FDW)**
  - Setup and configuration
  - `CREATE SERVER` and `CREATE FOREIGN TABLE`

---

### **6. Transactions**
- **Transaction Control**
  - `BEGIN`
  - `COMMIT`
  - `ROLLBACK`

- **Isolation Levels**
  - Read uncommitted
  - Read committed
  - Repeatable read
  - Serializable

- **Savepoints**
  - Nested transactions using `SAVEPOINT`

---

### **7. Extensions**
- **Common Extensions**
  - `PostGIS` for geographic data
  - `pgcrypto` for cryptographic functions
  - `hstore` for key-value storage
  - `uuid-ossp` for UUID generation

- **Management**
  - `CREATE EXTENSION`
  - Enabling/disabling extensions

---

### **8. JSON and JSONB**
- **JSON Operations**
  - JSON data type
  - JSONB for binary storage
  - JSON functions and operators (`->`, `->>`, `@>`)

- **Querying JSON**
  - Path queries
  - Indexing JSON (`GIN`)

---

### **9. Security**
- **Authentication**
  - Password-based authentication
  - Trust authentication
  - `pg_hba.conf`

- **SSL and Encryption**
  - Enabling SSL
  - Secure connections

- **Row-Level Security**
  - Policies (`CREATE POLICY`)
  - Enabling RLS

---

### **10. Replication and High Availability**
- **Replication Types**
  - Streaming replication
  - Logical replication
  - Synchronous vs. asynchronous

- **Clustering**
  - Failover
  - Load balancing

- **Tools**
  - `pg_basebackup`
  - `repmgr`

---

### **11. Performance Tuning**
- **Configuration**
  - `postgresql.conf`
  - Memory settings (`shared_buffers`, `work_mem`)
  - Query optimization settings (`effective_cache_size`)

- **Caching**
  - Disk and memory cache
  - Query cache strategies

- **Connection Pooling**
  - Using `PgBouncer`
  - Pool management

---

### **12. Miscellaneous**
- **Foreign Keys and Relationships**
  - Cascading updates and deletes
  - Deferred constraints

- **Inheritance**
  - Table inheritance
  - Parent-child table relationships

- **Time Zone Support**
  - `TIMESTAMP WITH TIME ZONE`
  - Conversions and functions

- **Event Triggers**
  - Database-wide triggers
  - Custom event handling

--- 
