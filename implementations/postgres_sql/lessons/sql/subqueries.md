## PostgreSQL – Subqueries

### Overview

A **subquery** in PostgreSQL is a **query nested inside another query**, used to provide intermediate results for filtering, calculation, or aggregation. Subqueries can appear in **SELECT, FROM, WHERE, or HAVING clauses**.

### Key Concepts

* **Purpose**

  * Break complex queries into manageable parts.
  * Filter, aggregate, or transform data based on the result of another query.
  * Enable dynamic and conditional data retrieval.

* **Types of Subqueries**

  * **Scalar Subquery**

    * Returns a **single value**.
    * Can be used in `SELECT` or comparison operations.

      ```sql
      SELECT name, (SELECT MAX(salary) FROM employees) AS max_salary
      FROM employees;
      ```

  * **Row Subquery**

    * Returns a **single row** with multiple columns.
    * Can be used with **row-wise comparisons**.

      ```sql
      SELECT *
      FROM employees
      WHERE (department_id, salary) = (SELECT department_id, MAX(salary) FROM employees GROUP BY department_id);
      ```

  * **Column Subquery**

    * Returns a **single column of values**.
    * Often used with `IN` or `NOT IN`.

      ```sql
      SELECT name
      FROM employees
      WHERE department_id IN (SELECT id FROM departments WHERE location = 'NY');
      ```

  * **Table Subquery**

    * Returns a **full table or set of rows**.
    * Used in the `FROM` clause as a **derived table or CTE**.

      ```sql
      SELECT dept, avg_salary
      FROM (SELECT department_id AS dept, AVG(salary) AS avg_salary FROM employees GROUP BY department_id) AS dept_avg
      WHERE avg_salary > 50000;
      ```

* **Correlated vs Non-Correlated Subqueries**

  * **Non-Correlated Subquery**

    * Executes **once** independently of the outer query.
  * **Correlated Subquery**

    * References **columns from the outer query** and executes **for each row**.

      ```sql
      SELECT name
      FROM employees e1
      WHERE salary > (SELECT AVG(salary) FROM employees e2 WHERE e1.department_id = e2.department_id);
      ```

* **Use Cases**

  * Filtering data with `WHERE` / `HAVING`.
  * Aggregating data before joining or comparison.
  * Dynamic calculations in `SELECT` statements.
  * Creating derived tables for complex queries.

* **Considerations**

  * Correlated subqueries can impact **performance**; use joins or CTEs when possible.
  * Always ensure subquery returns **expected cardinality** for correct results.
  * Can be combined with set operations for **complex data retrieval**.

### Summary

Subqueries in PostgreSQL are **nested queries** used for filtering, aggregation, and dynamic computation:

* Scalar, Row, Column, Table subqueries
* Correlated and Non-Correlated types
* Can appear in SELECT, FROM, WHERE, and HAVING clauses
* Useful for **breaking complex queries into logical, manageable components**

---
