## PostgreSQL – Grouping Sets / ROLLUP / CUBE

### Overview

**Grouping Sets, ROLLUP, and CUBE** in PostgreSQL are **advanced grouping features** that allow **multiple levels of aggregation** in a single query. They extend `GROUP BY` to produce **hierarchical, subtotal, or multidimensional summaries** efficiently.

### Key Concepts

* **Purpose**

  * Generate multiple aggregated results in **one query**.
  * Simplify complex aggregation queries.
  * Support **OLAP-style reporting** (business intelligence and analytics).

* **Grouping Sets**

  * Allows specifying **multiple groupings** in a single query.
  * Syntax:

    ```sql
    SELECT department_id, job_id, SUM(salary) AS total_salary
    FROM employees
    GROUP BY GROUPING SETS (
        (department_id, job_id),
        (department_id),
        (job_id),
        ()
    );
    ```
  * Produces aggregates for **all specified combinations**.
  * Empty parentheses `()` represent the **grand total**.

* **ROLLUP**

  * Generates **hierarchical subtotal aggregations** along the specified columns.
  * Syntax:

    ```sql
    SELECT department_id, job_id, SUM(salary) AS total_salary
    FROM employees
    GROUP BY ROLLUP(department_id, job_id);
    ```
  * Produces results in **top-down hierarchy**:

    * `(department_id, job_id)`
    * `(department_id)`
    * `()` – grand total
  * Simplifies queries compared to multiple `GROUPING SETS`.

* **CUBE**

  * Generates **all possible combinations** of the grouped columns.
  * Syntax:

    ```sql
    SELECT department_id, job_id, SUM(salary) AS total_salary
    FROM employees
    GROUP BY CUBE(department_id, job_id);
    ```
  * Produces aggregates for every possible combination:

    * `(department_id, job_id)`
    * `(department_id)`
    * `(job_id)`
    * `()` – grand total
  * Useful for **multidimensional analysis**.

* **GROUPING() Function**

  * Identifies whether a column in a grouping set is **aggregated or not**.

    ```sql
    SELECT department_id, job_id, SUM(salary),
           GROUPING(department_id) AS grp_dept,
           GROUPING(job_id) AS grp_job
    FROM employees
    GROUP BY ROLLUP(department_id, job_id);
    ```

* **Considerations**

  * Efficiently replaces **multiple UNION ALL queries**.
  * Works with **HAVING, ORDER BY, and window functions**.
  * Performance depends on table size and indexing.

### Summary

Grouping Sets, ROLLUP, and CUBE in PostgreSQL allow **advanced aggregation** in a single query:

* **Grouping Sets** – custom multiple groupings
* **ROLLUP** – hierarchical subtotals
* **CUBE** – all possible combinations (multidimensional totals)
* **GROUPING()** – identifies aggregated columns
* Enables **OLAP-style analytics** and reduces complex query duplication

---
