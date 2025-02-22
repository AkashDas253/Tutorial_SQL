## ANSI SQL cheatsheet

- **SQL Basics**  
  - Database & Schema  
  - Data Types  
  - NULL Handling  

- **SQL Statements**  
  - DDL (CREATE, ALTER, DROP)  
  - DML (INSERT, UPDATE, DELETE)  
  - DQL (SELECT)  
  - DCL (GRANT, REVOKE)  
  - TCL (COMMIT, ROLLBACK, SAVEPOINT)  

- **Constraints**  
  - Primary Key  
  - Foreign Key  
  - Unique  
  - Check  
  - Not Null  

- **Joins**  
  - INNER JOIN  
  - LEFT JOIN  
  - RIGHT JOIN  
  - FULL JOIN  
  - CROSS JOIN  
  - SELF JOIN  

- **Subqueries**  
  - Scalar Subquery  
  - Correlated Subquery  
  - Derived Tables  

- **Set Operations**  
  - UNION  
  - UNION ALL  
  - INTERSECT  
  - EXCEPT  

- **Aggregations**  
  - COUNT, SUM, AVG, MIN, MAX  
  - GROUP BY  
  - HAVING  

- **Window Functions**  
  - ROW_NUMBER()  
  - RANK(), DENSE_RANK()  
  - LEAD(), LAG()  

- **Indexes**  
  - Clustered Index  
  - Non-Clustered Index  

- **Transactions**  
  - ACID Properties  
  - Savepoints  
  - Isolation Levels  

- **Views & Materialized Views**  
  - Creating Views  
  - Updating Views  

- **Common Table Expressions (CTEs)**  
  - Recursive CTEs  
  - Non-Recursive CTEs  

- **Stored Procedures & Functions**  
  - User-Defined Functions  
  - Parameterized Procedures  

- **Triggers**  
  - BEFORE & AFTER Triggers  
  - Row-Level & Statement-Level Triggers  

- **Performance Optimization**  
  - Query Execution Plan  
  - Index Optimization  

---

## ANSI SQL Concepts and Subconcepts  

### Data Definition Language (DDL)  
Used to define and manage database schema.  

- **CREATE**: Defines new database objects.  
  - `CREATE TABLE`: Defines a new table.  
  - `CREATE VIEW`: Defines a virtual table.  
  - `CREATE INDEX`: Creates an index for faster searches.  
  - `CREATE DATABASE`: Defines a new database.  
- **ALTER**: Modifies existing database objects.  
  - `ALTER TABLE`: Modifies the structure of a table.  
  - `ALTER VIEW`: Modifies a view definition.  
- **DROP**: Deletes database objects.  
  - `DROP TABLE`: Removes a table.  
  - `DROP VIEW`: Removes a view.  
  - `DROP DATABASE`: Removes a database.  
  - `DROP INDEX`: Removes an index.  
- **TRUNCATE**: Deletes all rows from a table without logging individual row deletions.  

---

### Data Manipulation Language (DML)  
Used for managing data within schema objects.  

- **SELECT**: Retrieves data from the database.  
  - Subconcepts:  
    - Filtering: `WHERE`, `HAVING`.  
    - Ordering: `ORDER BY`.  
    - Grouping: `GROUP BY`.  
    - Joins: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL JOIN`, `CROSS JOIN`.  
    - Subqueries: Scalar, Correlated, and Nested subqueries.  
  - Functions:  
    - Aggregate: `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`.  
    - Scalar: `UPPER()`, `LOWER()`, `SUBSTRING()`, `ROUND()`.  
- **INSERT**: Adds new data to the database.  
  - `INSERT INTO ... VALUES`.  
  - `INSERT INTO ... SELECT`.  
- **UPDATE**: Modifies existing data.  
  - `UPDATE ... SET ... WHERE`.  
- **DELETE**: Removes specific data.  
  - `DELETE FROM ... WHERE`.  

---

### Data Control Language (DCL)  
Used to control access to data.  

- **GRANT**: Provides access to database objects.  
  - Permissions: `SELECT`, `INSERT`, `UPDATE`, `DELETE`.  
- **REVOKE**: Removes access to database objects.  
  - Permissions: `SELECT`, `INSERT`, `UPDATE`, `DELETE`.  

---

### Transaction Control Language (TCL)  
Used to manage database transactions.  

- **COMMIT**: Saves changes to the database.  
- **ROLLBACK**: Reverts changes made during a transaction.  
- **SAVEPOINT**: Sets a point in a transaction to which you can later roll back.  

---

### Constraints  
Used to enforce rules on data.  

- **PRIMARY KEY**: Uniquely identifies rows.  
- **FOREIGN KEY**: References a primary key in another table.  
- **UNIQUE**: Ensures all values in a column are unique.  
- **NOT NULL**: Prevents null values in a column.  
- **CHECK**: Ensures column values satisfy a condition.  
- **DEFAULT**: Assigns a default value if no value is provided.  

---

### Joins  
Combines rows from multiple tables.  

- **INNER JOIN**: Returns matching rows.  
- **LEFT JOIN**: Includes all rows from the left table and matching rows from the right.  
- **RIGHT JOIN**: Includes all rows from the right table and matching rows from the left.  
- **FULL JOIN**: Includes rows with matches in either table.  
- **CROSS JOIN**: Produces a Cartesian product.  

---

### Subqueries  
Queries within a query.  

- **Scalar Subquery**: Returns a single value.  
- **Multi-row Subquery**: Returns multiple rows.  
- **Correlated Subquery**: Depends on the outer query.  
- **Nested Subquery**: Subqueries inside other subqueries.  

---

### SQL Operators  
Used in filtering and conditions.  

| **Type**      | **Operators**                                                                                   |  
|---------------|-----------------------------------------------------------------------------------------------|  
| Comparison    | `=`, `<>`, `!=`, `<`, `>`, `<=`, `>=`, `BETWEEN`, `IN`, `LIKE`, `IS NULL`.                     |  
| Logical       | `AND`, `OR`, `NOT`.                                                                           |  
| Arithmetic    | `+`, `-`, `*`, `/`, `%`.                                                                      |  
| Bitwise       | `&`, `|`, `^`, `~`, `<<`, `>>`.                                                               |  

---

### SQL Functions  
Used to perform operations on data.  

| **Function Type** | **Functions**                                                                                  |  
|-------------------|-----------------------------------------------------------------------------------------------|  
| Aggregate         | `SUM`, `AVG`, `COUNT`, `MIN`, `MAX`.                                                          |  
| Scalar            | `UPPER`, `LOWER`, `LENGTH`, `SUBSTRING`, `ROUND`, `CONCAT`.                                   |  
| Date/Time         | `NOW`, `CURDATE`, `DATEDIFF`, `DATE_ADD`, `DATE_SUB`.                                         |  
| Numeric           | `ABS`, `CEIL`, `FLOOR`, `MOD`, `POWER`.                                                      |  

---

### Indexing  
Improves query performance.  

- **CREATE INDEX**: Adds an index.  
- **DROP INDEX**: Removes an index.  
- **UNIQUE INDEX**: Ensures indexed columns have unique values.  

---

### Views  
Virtual tables representing query results.  

- **CREATE VIEW**: Defines a view.  
- **ALTER VIEW**: Modifies a view.  
- **DROP VIEW**: Deletes a view.  

---
