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