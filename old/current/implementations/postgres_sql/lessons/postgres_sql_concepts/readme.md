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

