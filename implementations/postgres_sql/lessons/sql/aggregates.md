## PostgreSQL – Aggregate Functions

### Overview

**Aggregate functions** in PostgreSQL perform **calculations on a set of rows** and return a **single summarizing value**. They are commonly used with `GROUP BY` to **summarize data** in reports and analytics.

### Key Concepts

* **Purpose**

  * Summarize or compute statistics over multiple rows.
  * Support reporting, analytics, and data aggregation.
  * Can be combined with `GROUP BY` and `HAVING` for detailed aggregation.

* **Common Aggregate Functions**

  * **COUNT()**

    * Counts rows or non-NULL values.

      ```sql
      SELECT COUNT(*) FROM employees;
      SELECT COUNT(salary) FROM employees;
      ```
  * **SUM()**

    * Calculates the total sum of a numeric column.

      ```sql
      SELECT SUM(salary) FROM employees;
      ```
  * **AVG()**

    * Computes the average value of a numeric column.

      ```sql
      SELECT AVG(salary) FROM employees;
      ```
  * **MIN() / MAX()**

    * Returns the minimum or maximum value of a column.

      ```sql
      SELECT MIN(salary), MAX(salary) FROM employees;
      ```
  * **ARRAY\_AGG()**

    * Returns an array of values from a column.

      ```sql
      SELECT ARRAY_AGG(name) FROM employees;
      ```
  * **STRING\_AGG()**

    * Concatenates strings from multiple rows with a delimiter.

      ```sql
      SELECT STRING_AGG(name, ', ') FROM employees;
      ```
  * **BOOL\_AND() / BOOL\_OR()**

    * Returns TRUE if all/any values in a boolean column satisfy the condition.

      ```sql
      SELECT BOOL_AND(active) FROM employees;
      SELECT BOOL_OR(active) FROM employees;
      ```

* **Grouping**

  * `GROUP BY` is used to **aggregate rows based on one or more columns**.

    ```sql
    SELECT department_id, AVG(salary)
    FROM employees
    GROUP BY department_id;
    ```
  * `HAVING` filters aggregated results:

    ```sql
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
    HAVING AVG(salary) > 50000;
    ```

* **Window vs Aggregate Functions**

  * **Aggregate functions** collapse rows into a single value per group.
  * **Window functions** maintain row-level results while performing aggregation.

* **Considerations**

  * Aggregate functions ignore **NULL values** by default (except COUNT(\*) counts all rows).
  * Proper indexing on grouping columns improves performance.
  * Can be combined with **DISTINCT** to aggregate unique values:

    ```sql
    SELECT COUNT(DISTINCT department_id) FROM employees;
    ```

### Summary

Aggregate functions in PostgreSQL provide **summarized insights over multiple rows**:

* COUNT, SUM, AVG, MIN, MAX, ARRAY\_AGG, STRING\_AGG, BOOL\_AND, BOOL\_OR
* Used with `GROUP BY` for grouped aggregation
* `HAVING` filters aggregated results
* Key tool for **reporting, analytics, and statistical computation**

---
