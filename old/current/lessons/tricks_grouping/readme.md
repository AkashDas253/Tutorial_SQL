## **GROUP BY** and **HAVING**

### 1. **GROUP BY Clause**

The `GROUP BY` clause is used to aggregate rows that have the same values in specified columns into summary rows, often used with aggregate functions (`COUNT()`, `SUM()`, `AVG()`, etc.).

#### **Basic GROUP BY Syntax**

```sql
-- Trick: Grouping rows by column(s) and applying an aggregate function
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

**Use when**: You want to group your data based on certain columns, like counting employees per department.

---

### 2. **GROUP BY with Aggregation Functions**

```sql
-- Trick: Grouping and applying aggregate functions like SUM, AVG, MAX, etc.
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

**Use when**: You need to perform aggregation (e.g., average salary) for each group of data (e.g., each department).

---

### 3. **GROUP BY Multiple Columns**

```sql
-- Trick: Group by more than one column to get sub-groupings
SELECT department, job_title, COUNT(*) AS employee_count
FROM employees
GROUP BY department, job_title;
```

**Use when**: You need to group data by multiple columns (e.g., department and job title) for a more detailed aggregation.

---

### 4. **GROUP BY with ORDER BY**

```sql
-- Trick: Group by a column and order the results by an aggregate function
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department
ORDER BY total_salary DESC;
```

**Use when**: You want to order the result of your grouped data, such as sorting departments by the total salary in descending order.

---

### 5. **GROUP BY with DISTINCT**

```sql
-- Trick: GROUP BY with DISTINCT values (if you want unique results in certain fields)
SELECT department, COUNT(DISTINCT job_title) AS unique_job_titles
FROM employees
GROUP BY department;
```

**Use when**: You need to count or aggregate only distinct values within each group.

---

### 6. **GROUP BY with COUNT()**

```sql
-- Trick: Using COUNT to count rows within each group
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

**Use when**: You need to count the number of rows in each group, for example, counting employees in each department.

---

### 7. **GROUP BY with NULL Handling**

```sql
-- Trick: Group by columns that may contain NULL values
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department
WITH ROLLUP;  -- Adds a summary row with NULL for department
```

**Use when**: You want to include summary rows for groups, even when a column may have NULL values.

---

### 8. **GROUP BY with HAVING**

The `HAVING` clause is used to filter groups based on a condition. Unlike `WHERE`, which filters individual rows, `HAVING` filters groups after the aggregation.

#### **Basic HAVING Syntax**

```sql
-- Trick: Using HAVING to filter groups after applying aggregate functions
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

**Use when**: You need to filter groups based on an aggregate function (e.g., only departments with more than 5 employees).

---

### 9. **HAVING with Aggregate Functions**

```sql
-- Trick: Use HAVING to filter based on aggregated values (e.g., SUM, AVG)
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

**Use when**: You want to filter groups where the aggregated value (e.g., average salary) exceeds a certain threshold.

---

### 10. **HAVING with Multiple Conditions**

```sql
-- Trick: Using multiple conditions in HAVING for more complex filtering
SELECT department, COUNT(*) AS employee_count, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING COUNT(*) > 5 AND AVG(salary) > 50000;
```

**Use when**: You want to apply multiple filters on grouped data, such as counting employees and checking if the average salary exceeds a value.

---

### 11. **HAVING with a Subquery**

```sql
-- Trick: Using HAVING with a subquery for advanced filtering
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > (SELECT COUNT(*) FROM employees WHERE department = 'HR');
```

**Use when**: You need to filter groups based on a comparison with another group or a subquery result.

---

### 12. **GROUP BY with ROLLUP or CUBE**

The `ROLLUP` and `CUBE` extensions to `GROUP BY` provide additional summary rows in the result set. `ROLLUP` generates subtotals and a grand total, while `CUBE` provides a more detailed cross-tabulation.

#### **Using ROLLUP**

```sql
-- Trick: GROUP BY with ROLLUP for subtotal and grand total
SELECT department, job_title, COUNT(*) AS employee_count
FROM employees
GROUP BY department, job_title WITH ROLLUP;
```

**Use when**: You want to include subtotal and grand total rows in your aggregation.

#### **Using CUBE**

```sql
-- Trick: GROUP BY with CUBE to get all combinations of grouping
SELECT department, job_title, COUNT(*) AS employee_count
FROM employees
GROUP BY department, job_title WITH CUBE;
```

**Use when**: You need all possible combinations of groupings, providing a comprehensive summary across multiple dimensions.

---

### Key Tips for **GROUP BY** and **HAVING**:

* **GROUP BY** aggregates data based on columns, while **HAVING** filters based on aggregate results.
* **HAVING** is applied after the aggregation, while **WHERE** filters rows before aggregation.
* Use **GROUP BY** for summaries (e.g., counting employees, summing sales), and **HAVING** when you want to filter these summaries.
* When grouping by multiple columns, the result will have one row per unique combination of those columns.
* **ROLLUP** and **CUBE** are useful for generating subtotals and cross-tabulations but can result in more rows than expected.
* Use **COUNT(DISTINCT)** for counting unique values in groups.

---
