# **Comprehensive Notes on PostgreSQL (PGSQL) SQL Statements**  

## **SQL Statement Categories**  

PostgreSQL SQL statements are divided into several categories based on their purpose:  

| **Category**         | **Description** |
|----------------------|---------------|
| **Data Definition Language (DDL)** | Defines database objects like tables, indexes, views, and schemas. |
| **Data Manipulation Language (DML)** | Modifies data in tables (INSERT, UPDATE, DELETE, SELECT). |
| **Transaction Control Language (TCL)** | Manages transactions (COMMIT, ROLLBACK, SAVEPOINT). |
| **Data Query Language (DQL)** | Retrieves data from the database (SELECT). |
| **Data Control Language (DCL)** | Manages user permissions and access (GRANT, REVOKE). |
| **Procedural Language (PL/pgSQL)** | Defines stored procedures, functions, and triggers. |

---

## **Data Definition Language (DDL)**
DDL statements define and modify the structure of database objects.

| **Statement** | **Description** |
|--------------|---------------|
| `CREATE DATABASE db_name;` | Creates a new database. |
| `DROP DATABASE db_name;` | Deletes a database. |
| `CREATE SCHEMA schema_name;` | Defines a schema within a database. |
| `DROP SCHEMA schema_name;` | Deletes a schema. |
| `CREATE TABLE table_name (...);` | Creates a table. |
| `DROP TABLE table_name;` | Deletes a table. |
| `ALTER TABLE table_name ADD COLUMN col_name data_type;` | Adds a column to a table. |
| `ALTER TABLE table_name DROP COLUMN col_name;` | Removes a column. |
| `TRUNCATE TABLE table_name;` | Removes all rows from a table without logging individual row deletions. |
| `CREATE INDEX index_name ON table_name (column_name);` | Creates an index on a column. |
| `DROP INDEX index_name;` | Removes an index. |

---

## **Data Manipulation Language (DML)**
DML statements modify data in tables.

| **Statement** | **Description** |
|--------------|---------------|
| `INSERT INTO table_name (col1, col2) VALUES (val1, val2);` | Inserts a new row. |
| `INSERT INTO table_name DEFAULT VALUES;` | Inserts a row with default values. |
| `UPDATE table_name SET col1 = val1 WHERE condition;` | Updates rows based on a condition. |
| `DELETE FROM table_name WHERE condition;` | Deletes specific rows. |
| `DELETE FROM table_name;` | Deletes all rows without removing the table structure. |

---

## **Data Query Language (DQL)**
DQL retrieves data from tables.

| **Statement** | **Description** |
|--------------|---------------|
| `SELECT * FROM table_name;` | Retrieves all columns and rows. |
| `SELECT col1, col2 FROM table_name WHERE condition;` | Retrieves specific columns with a filter. |
| `SELECT DISTINCT col1 FROM table_name;` | Retrieves unique values. |
| `SELECT * FROM table_name ORDER BY col1 ASC/DESC;` | Sorts results in ascending/descending order. |
| `SELECT * FROM table1 INNER JOIN table2 ON condition;` | Joins two tables based on a condition. |
| `SELECT COUNT(*) FROM table_name;` | Returns the total row count. |
| `SELECT col1 FROM table_name GROUP BY col1;` | Groups rows based on column values. |
| `SELECT col1, SUM(col2) FROM table_name GROUP BY col1 HAVING condition;` | Filters grouped results. |
| `SELECT * FROM table_name LIMIT 10;` | Retrieves a limited number of rows. |
| `SELECT * FROM table_name OFFSET 5;` | Skips the first 5 rows and retrieves the rest. |

---

## **Transaction Control Language (TCL)**
TCL manages transactions.

| **Statement** | **Description** |
|--------------|---------------|
| `BEGIN;` | Starts a transaction. |
| `COMMIT;` | Saves all changes within a transaction. |
| `ROLLBACK;` | Undoes all changes since the last `BEGIN`. |
| `SAVEPOINT savepoint_name;` | Creates a checkpoint within a transaction. |
| `ROLLBACK TO SAVEPOINT savepoint_name;` | Rolls back to a specific checkpoint. |
| `RELEASE SAVEPOINT savepoint_name;` | Deletes a savepoint. |

---

## **Data Control Language (DCL)**
DCL statements control access permissions.

| **Statement** | **Description** |
|--------------|---------------|
| `GRANT SELECT ON table_name TO user_name;` | Grants read access to a user. |
| `GRANT ALL PRIVILEGES ON table_name TO user_name;` | Grants all permissions. |
| `REVOKE SELECT ON table_name FROM user_name;` | Removes read access from a user. |
| `REVOKE ALL PRIVILEGES ON table_name FROM user_name;` | Revokes all permissions. |

---

## **Procedural Language (PL/pgSQL)**
PL/pgSQL enables stored procedures and functions.

| **Statement** | **Description** |
|--------------|---------------|
| `CREATE FUNCTION function_name(...) RETURNS return_type AS $$ BEGIN ... END; $$ LANGUAGE plpgsql;` | Creates a function. |
| `DROP FUNCTION function_name;` | Deletes a function. |
| `CREATE PROCEDURE procedure_name(...) AS $$ BEGIN ... END; $$ LANGUAGE plpgsql;` | Creates a procedure. |
| `CALL procedure_name(...);` | Executes a procedure. |

---

## **Key Takeaways**
- **DDL** defines database structures.  
- **DML** modifies data in tables.  
- **DQL** retrieves data with `SELECT`.  
- **TCL** manages transactions for data consistency.  
- **DCL** controls user access and security.  
