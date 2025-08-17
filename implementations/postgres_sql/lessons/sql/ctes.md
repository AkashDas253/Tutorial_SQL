## PostgreSQL – Common Table Expressions (CTEs)

### Overview

A **Common Table Expression (CTE)** is a **temporary named result set** that can be referenced within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement. CTEs help **structure complex queries**, improve readability, and enable **recursive queries**.

### Key Concepts

* **Purpose**

  * Simplify **complex queries** with nested subqueries.
  * Improve **readability and maintainability**.
  * Support **recursive queries** for hierarchical or iterative data.

* **Syntax**

  ```sql
  WITH cte_name (column_list) AS (
      subquery
  )
  SELECT *
  FROM cte_name;
  ```

* **Types of CTEs**

  * **Non-Recursive CTE**

    * Standard temporary result set.
    * Can be referenced multiple times in the main query.

      ```sql
      WITH dept_avg AS (
          SELECT department_id, AVG(salary) AS avg_salary
          FROM employees
          GROUP BY department_id
      )
      SELECT e.name, e.salary, d.avg_salary
      FROM employees e
      JOIN dept_avg d
      ON e.department_id = d.department_id;
      ```
  * **Recursive CTE**

    * Refers to itself to handle **hierarchical or iterative data**.
    * Requires **anchor member** and **recursive member**.

      ```sql
      WITH RECURSIVE subordinates AS (
          SELECT id, name, manager_id
          FROM employees
          WHERE manager_id IS NULL  -- anchor member

          UNION ALL

          SELECT e.id, e.name, e.manager_id
          FROM employees e
          JOIN subordinates s ON e.manager_id = s.id  -- recursive member
      )
      SELECT * FROM subordinates;
      ```

* **Key Features**

  * Can be **chained** (multiple CTEs separated by commas).
  * CTEs are **read-only** within the query.
  * Can improve performance for **complex subqueries**, but may materialize results, affecting memory for large datasets.
  * Can be used with `INSERT`, `UPDATE`, `DELETE` to simplify **data manipulation workflows**.

* **Considerations**

  * Recursive CTEs must have a **termination condition** to avoid infinite loops.
  * Large CTEs can impact performance; in some cases, **temporary tables** may be more efficient.
  * `MATERIALIZED` keyword can be used in PostgreSQL 12+ to **force CTE evaluation** and reuse results.

### Summary

CTEs in PostgreSQL are **temporary named result sets** for query structuring and recursion:

* Non-recursive: simplify subqueries and joins
* Recursive: handle hierarchical or iterative data
* Chained, reusable, and usable in SELECT/INSERT/UPDATE/DELETE
* Improve **readability, maintainability, and complex query logic**

---
