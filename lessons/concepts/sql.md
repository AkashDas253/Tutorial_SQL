## SQL Concepts and Subconcepts

### SQL Fundamentals

* SQL Overview

  * Definition and purpose
  * Declarative programming
  * ANSI SQL standard
  * SQL compliance levels
* SQL Categories

  * DDL (Data Definition Language)
  * DML (Data Manipulation Language)
  * DCL (Data Control Language)
  * TCL (Transaction Control Language)
  * DQL (Data Query Language)
  * SQL Extensions (procedural, analytic, recursive)

---

### Data Definition Language (DDL)

* CREATE Statements

  * CREATE DATABASE
  * CREATE SCHEMA / Namespace
  * CREATE TABLE

    * Column definitions
    * Data types
    * Constraints (PK, FK, UNIQUE, NOT NULL, CHECK, DEFAULT)
  * CREATE VIEW
  * CREATE INDEX

    * Unique / Non-unique
    * Clustered / Non-clustered
    * Functional / Partial / Expression-based
  * CREATE SEQUENCE
  * CREATE TRIGGER
  * CREATE PROCEDURE / FUNCTION (conceptual)
  * CREATE SYNONYM / ALIAS
* ALTER Statements

  * ALTER TABLE

    * Add, modify, drop columns
    * Rename columns / table
    * Add / drop constraints
  * ALTER VIEW
  * ALTER INDEX (conceptual)
  * ALTER SCHEMA
* DROP Statements

  * DROP DATABASE / SCHEMA
  * DROP TABLE
  * DROP VIEW
  * DROP INDEX
  * DROP SEQUENCE / TRIGGER / FUNCTION / PROCEDURE
* TRUNCATE TABLE
* RENAME (tables, columns, objects)
* Constraints

  * PRIMARY KEY
  * FOREIGN KEY
  * UNIQUE
  * NOT NULL
  * CHECK
  * DEFAULT
  * Composite keys
  * Referential actions (CASCADE, SET NULL, NO ACTION, RESTRICT)

---

### Data Manipulation Language (DML)

* INSERT

  * Single-row insert
  * Multi-row insert
  * INSERT with SELECT
  * INSERT IGNORE / ON DUPLICATE / UPSERT (conceptual)
* UPDATE

  * Single / multiple columns
  * Conditional update (WHERE)
  * Update with subqueries
* DELETE

  * Conditional delete
  * DELETE ALL (truncate vs delete)
* MERGE / UPSERT (conceptual)
* RETURNING / OUTPUT (conceptual, for modified rows)

---

### Data Query Language (DQL)

* SELECT

  * Column selection, expressions
  * Aliases (column & table)
  * DISTINCT
  * Wildcards (\*)
* Filtering

  * WHERE clause

    * Comparison operators (=, <>, >, >=, <, <=)
    * Logical operators (AND, OR, NOT)
    * Pattern matching (LIKE, SIMILAR TO)
    * IN / NOT IN
    * BETWEEN / NOT BETWEEN
    * IS NULL / IS NOT NULL
    * EXISTS / NOT EXISTS
* Joins

  * INNER JOIN
  * OUTER JOIN (LEFT, RIGHT, FULL)
  * CROSS JOIN
  * SELF JOIN
  * NATURAL JOIN (conceptual)
* Aggregations

  * COUNT, SUM, AVG, MIN, MAX
  * GROUP BY
  * HAVING
  * GROUPING SETS, ROLLUP, CUBE (conceptual)
* Set Operations

  * UNION / UNION ALL
  * INTERSECT
  * EXCEPT / MINUS
* Subqueries

  * Scalar
  * Correlated
  * Nested / multi-level
* Sorting

  * ORDER BY (ASC / DESC)
  * NULLS FIRST / LAST (conceptual)
* Limiting

  * LIMIT / OFFSET / FETCH / TOP
* Window / Analytic Functions (conceptual)

  * ROW\_NUMBER, RANK, DENSE\_RANK, NTILE
  * LEAD, LAG, FIRST\_VALUE, LAST\_VALUE
  * PARTITION BY
* Expressions

  * Arithmetic
  * String
  * Date / Time
  * Boolean
  * CASE expressions
* Functions

  * Scalar

    * Numeric
    * String
    * Date / Time
    * Conversion (CAST / CONVERT)
    * Type-specific
  * Aggregate

    * COUNT, SUM, AVG, MIN, MAX
  * Analytic / Window (conceptual)
  * Conditional (IFNULL, COALESCE, NULLIF, NVL)
* Common Table Expressions (CTEs)

  * Recursive CTEs (conceptual)
* Views (conceptual as part of queries)

  * Updatable views
  * Materialized views

---

### Data Control Language (DCL)

* GRANT

  * Privileges on tables, views, schemas
  * Column-level privileges
  * Roles and users
  * Granting with grant option
* REVOKE

  * Removing privileges
* Roles / Groups / Users
* Security & Access Control (conceptual)

---

### Transaction Control Language (TCL)

* Transactions

  * BEGIN / START TRANSACTION
  * COMMIT
  * ROLLBACK
* Savepoints
* Transaction Isolation Levels

  * READ UNCOMMITTED
  * READ COMMITTED
  * REPEATABLE READ
  * SERIALIZABLE
* ACID properties

  * Atomicity
  * Consistency
  * Isolation
  * Durability
* Locking and concurrency (conceptual)

  * Row-level locks
  * Table-level locks
  * Deadlocks
* Implicit vs explicit transactions

---

### Data Types (conceptual, general)

* Numeric

  * INTEGER / INT / SMALLINT / BIGINT
  * DECIMAL / NUMERIC / FLOAT / REAL / DOUBLE
* Character

  * CHAR, VARCHAR, TEXT, CLOB
* Date / Time

  * DATE, TIME, TIMESTAMP, INTERVAL
* Boolean / Logical
* Binary

  * BINARY, VARBINARY, BLOB
* UUID / GUID (conceptual)
* JSON / XML / JSONB / Structured types (conceptual)
* Enumerated types (ENUM)
* User-defined types (UDT, conceptual)

---

### Referential Integrity

* Primary key / foreign key relationships
* Cascading actions

  * ON DELETE CASCADE / SET NULL / RESTRICT / NO ACTION
  * ON UPDATE CASCADE / SET NULL / RESTRICT / NO ACTION
* Self-referencing keys
* Composite keys

---

### Indexing & Performance

* Index types

  * Unique / Non-unique
  * Clustered / Non-clustered
  * Functional / Partial / Expression-based
  * Bitmap (conceptual)
* Index usage in queries
* Constraints vs Index interaction
* Query optimization concepts (conceptual)

  * Execution plan
  * Cost-based optimization
  * Statistics and selectivity

---

### Stored Objects & Procedural SQL

* Stored Procedures
* Functions
* Triggers

  * BEFORE / AFTER / INSTEAD OF
  * Row-level / Statement-level
* Cursors

  * Implicit
  * Explicit
* Sequences / Generators
* Packages / Modules (conceptual)
* Exception handling (conceptual)

  * TRY/CATCH / DECLARE HANDLER
* Loops, conditionals (conceptual procedural SQL)

---

### Advanced SQL Concepts

* Recursive queries
* Hierarchical queries (CONNECT BY, conceptually)
* Pivot / Unpivot (conceptual)
* Temporary tables / session tables
* Transactions across distributed systems (conceptual)
* Multi-version concurrency control (MVCC, conceptual)
* Partitioning

  * Table partitioning
  * Index partitioning
  * Range, List, Hash, Composite (conceptual)
* Sharding / Distributed SQL (conceptual)
* Full-text search (conceptual)
* Views & materialized views
* Audit / logging triggers (conceptual)
* Data warehousing constructs (conceptual)

  * Star / snowflake schema
  * Fact / dimension tables

---

### Nulls & Special Values

* NULL

  * Handling in expressions
  * IS NULL / IS NOT NULL
  * Null propagation rules
* DEFAULT values
* Special constants (CURRENT\_DATE, CURRENT\_TIMESTAMP, SYSTEM\_USER, etc.)

---
