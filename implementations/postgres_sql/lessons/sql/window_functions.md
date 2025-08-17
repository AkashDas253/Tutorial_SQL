## PostgreSQL – Window Functions

### Overview

**Window functions** in PostgreSQL perform calculations **across a set of table rows related to the current row** without collapsing the result into a single output row. They are used for **ranking, running totals, moving averages, and analytics**.

### Key Concepts

* **Purpose**

  * Perform **aggregate and ranking calculations** over a subset of rows (window).
  * Maintain **row-level details** while computing analytics.
  * Useful for **reporting, trend analysis, and advanced queries**.

* **Syntax**

  ```sql
  function_name(arguments) OVER (
      [PARTITION BY column_list]
      [ORDER BY column_list]
      [ROWS frame_specification]
  )
  ```

* **Components**

  * **Function**: Aggregate or ranking function (e.g., `ROW_NUMBER()`, `RANK()`, `SUM()`, `AVG()`, `LEAD()`, `LAG()`).
  * **OVER() clause**: Defines the window for calculation.

    * **PARTITION BY** – Divides rows into **groups**.
    * **ORDER BY** – Determines **ordering** within each partition.
    * **ROWS/RANGE** – Defines a **frame of rows** relative to the current row.

* **Common Window Functions**

  * **Ranking Functions**

    * `ROW_NUMBER()` – Sequential row number within a partition.
    * `RANK()` – Rank with gaps for ties.
    * `DENSE_RANK()` – Rank without gaps for ties.
    * `NTILE(n)` – Divides rows into `n` buckets.
  * **Aggregate Functions**

    * `SUM()`, `AVG()`, `MIN()`, `MAX()`, `COUNT()` over a window.
  * **Value Functions**

    * `LEAD()` – Access the value of the next row.
    * `LAG()` – Access the value of the previous row.
    * `FIRST_VALUE()`, `LAST_VALUE()` – Retrieve first/last value in the window.

* **Examples**

  ```sql
  SELECT name, department_id, salary,
         RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS dept_rank
  FROM employees;

  SELECT name, salary,
         AVG(salary) OVER (ORDER BY salary ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg
  FROM employees;
  ```

* **Use Cases**

  * Ranking employees by salary within departments.
  * Calculating running totals, moving averages, or cumulative sums.
  * Comparing current row values to previous/next rows.
  * Analytics and reporting without grouping rows.

* **Considerations**

  * Window functions do **not reduce the number of rows**.
  * Can be combined with `ORDER BY` for precise calculations.
  * Large partitions may affect **performance**, indexing may help.

### Summary

Window functions in PostgreSQL provide **advanced analytics capabilities**:

* ROW\_NUMBER, RANK, DENSE\_RANK, NTILE, SUM, AVG, LEAD, LAG, FIRST\_VALUE, LAST\_VALUE
* Use `PARTITION BY` and `ORDER BY` to define windows
* Maintain **row-level granularity** while computing aggregates and ranks
* Ideal for **reporting, trend analysis, and analytical queries**

---
