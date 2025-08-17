## PostgreSQL – Joins

### Overview

A **join** in PostgreSQL is an operation that **combines rows from two or more tables** based on a related column between them. Joins are essential for **relational data retrieval** and support complex queries.

### Key Concepts

* **Purpose**

  * Retrieve data from multiple tables in a **single query**.
  * Enforce relationships between tables using **foreign keys** or common columns.
  * Enable aggregation and reporting across tables.

* **Types of Joins**

  * **INNER JOIN**

    * Returns rows **that have matching values** in both tables.
    * Syntax:

      ```sql
      SELECT *
      FROM table1
      INNER JOIN table2
      ON table1.column = table2.column;
      ```
  * **LEFT (OUTER) JOIN**

    * Returns all rows from the **left table**, and matching rows from the right table.
    * Non-matching right table rows return **NULL**.

      ```sql
      SELECT *
      FROM table1
      LEFT JOIN table2
      ON table1.column = table2.column;
      ```
  * **RIGHT (OUTER) JOIN**

    * Returns all rows from the **right table**, and matching rows from the left table.
    * Non-matching left table rows return **NULL**.

      ```sql
      SELECT *
      FROM table1
      RIGHT JOIN table2
      ON table1.column = table2.column;
      ```
  * **FULL (OUTER) JOIN**

    * Returns rows **when there is a match in one of the tables**.
    * Non-matching rows from either table appear with **NULL** in missing columns.

      ```sql
      SELECT *
      FROM table1
      FULL OUTER JOIN table2
      ON table1.column = table2.column;
      ```
  * **CROSS JOIN**

    * Returns the **Cartesian product** of two tables (all combinations).

      ```sql
      SELECT *
      FROM table1
      CROSS JOIN table2;
      ```
  * **SELF JOIN**

    * Joins a table with **itself**, typically using table aliases.

      ```sql
      SELECT a.id, b.id
      FROM employees a
      INNER JOIN employees b
      ON a.manager_id = b.id;
      ```

* **Join Conditions**

  * **Equi-join** – Matching columns using `=`.
  * **Non-equi join** – Matching columns using `<`, `>`, `BETWEEN`, etc.
  * **Natural Join** – Automatically joins using columns with the **same name**.
  * **Using Clause** – Simplifies join when column names are the same:

    ```sql
    SELECT *
    FROM table1
    JOIN table2 USING (column_name);
    ```

* **Considerations**

  * Join performance depends on **indexes and table size**.
  * Large joins may require **query optimization**.
  * Outer joins may introduce **NULLs**, affecting aggregate functions and conditions.

### Summary

Joins in PostgreSQL are used to **combine and relate data across tables**:

* INNER, LEFT, RIGHT, FULL, CROSS, SELF, NATURAL, USING
* Enable relational querying and reporting
* Proper indexing and conditions improve performance and correctness

---
