## Aggregate Functions in MySQL

**Aggregate functions** perform calculations on a set of values and return a single value. Commonly used in `SELECT` statements with `GROUP BY`, `HAVING`, or without grouping for overall summaries.

--- 

### 🔹 Inner Index

* [List of Aggregate Functions](#list-of-aggregate-functions)
* [Usage with SELECT](#usage-with-select)
* [Usage with GROUP BY](#usage-with-group-by)
* [Usage with HAVING](#usage-with-having)
* [Usage in Subqueries](#usage-in-subqueries)
* [Usage Scenarios](#usage-scenarios)

---

### List of Aggregate Functions

| Function             | Description                           | NULLs Included |
| -------------------- | ------------------------------------- | -------------- |
| `COUNT()`            | Returns number of non-NULL values     | No             |
| `SUM()`              | Returns total sum of values           | No             |
| `AVG()`              | Returns average of values             | No             |
| `MIN()`              | Returns minimum value                 | Yes            |
| `MAX()`              | Returns maximum value                 | Yes            |
| `GROUP_CONCAT()`     | Returns concatenated string of values | No             |
| `STD()` / `STDDEV()` | Returns standard deviation of values  | No             |
| `VAR_SAMP()`         | Returns sample variance               | No             |

---

### Usage with SELECT

**Syntax:**

```sql
SELECT COUNT(*) AS total_employees FROM employees;
SELECT AVG(salary) FROM employees;
SELECT MIN(hire_date) FROM employees;
```

---

### Usage with GROUP BY

**Syntax:**

```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;
```

---

### Usage with HAVING

Used to filter grouped rows based on aggregate results.

**Syntax:**

```sql
SELECT department_id, COUNT(*) AS emp_count
FROM employees
GROUP BY department_id
HAVING emp_count > 5;
```

---

### Usage in Subqueries

**Syntax:**

```sql
SELECT name FROM employees
WHERE salary = (
  SELECT MAX(salary) FROM employees
);
```

---

### Usage Scenarios

* **Total Orders:**

  ```sql
  SELECT COUNT(*) FROM orders;
  ```

* **Average Salary per Department:**

  ```sql
  SELECT department_id, AVG(salary) FROM employees GROUP BY department_id;
  ```

* **Departments with High Average Salary:**

  ```sql
  SELECT department_id
  FROM employees
  GROUP BY department_id
  HAVING AVG(salary) > 50000;
  ```

* **Concatenate Product Names:**

  ```sql
  SELECT GROUP_CONCAT(name) FROM products;
  ```

---

### Notes

* `COUNT(*)` counts all rows, including NULLs.
* `COUNT(column)` ignores NULL values.
* Use `DISTINCT` to eliminate duplicates:

  ```sql
  SELECT COUNT(DISTINCT department_id) FROM employees;
  ```

---

### Conclusion

Aggregate functions are essential for summarizing and analyzing data in MySQL. They are frequently used with grouping, filtering, and subqueries to produce meaningful insights.

---
