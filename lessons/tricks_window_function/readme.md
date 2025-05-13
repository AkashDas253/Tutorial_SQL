## 🪟 **Window Functions Tricks in SQL**

### 1. **Basic Window Function (ROW\_NUMBER)**

```sql
-- Trick: Assign row numbers to results
SELECT name, salary, 
       ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_num
FROM employees;
```

**Use when**: You need to assign a unique sequential number to each row, based on an ordering criterion.

---

### 2. **RANK and DENSE\_RANK**

```sql
-- Trick: Rank employees based on salary (ties get the same rank, with gaps for RANK)
SELECT name, salary, 
       RANK() OVER (ORDER BY salary DESC) AS rank
FROM employees;

-- Trick: Dense rank (ties get the same rank, without gaps)
SELECT name, salary, 
       DENSE_RANK() OVER (ORDER BY salary DESC) AS dense_rank
FROM employees;
```

**Use when**: You want to assign ranks to rows and handle ties in different ways.

---

### 3. **NTILE (Divide Data into N Buckets)**

```sql
-- Trick: Divide employees into 4 equal salary groups (quartiles)
SELECT name, salary, 
       NTILE(4) OVER (ORDER BY salary DESC) AS quartile
FROM employees;
```

**Use when**: You want to divide your data into a specific number of buckets or groups.

---

### 4. **PARTITION BY with Window Functions**

```sql
-- Trick: Rank employees within each department separately
SELECT department, name, salary, 
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
FROM employees;
```

**Use when**: You need to perform window functions partitioned by certain columns (like by department, region, etc.).

---

### 5. **SUM with OVER (Running Total)**

```sql
-- Trick: Calculate the running total of salaries
SELECT name, salary, 
       SUM(salary) OVER (ORDER BY salary) AS running_total
FROM employees;
```

**Use when**: You need to calculate a cumulative sum or running total.

---

### 6. **AVG with OVER (Moving Average)**

```sql
-- Trick: Calculate a moving average over the last 3 rows of salaries
SELECT name, salary, 
       AVG(salary) OVER (ORDER BY salary ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg
FROM employees;
```

**Use when**: You need a moving or sliding average over a set number of rows.

---

### 7. **LEAD and LAG (Access Next/Previous Row’s Data)**

```sql
-- Trick: Get next and previous salary values
SELECT name, salary, 
       LEAD(salary) OVER (ORDER BY salary) AS next_salary,
       LAG(salary) OVER (ORDER BY salary) AS prev_salary
FROM employees;
```

**Use when**: You need to access data from the next or previous row without using self-joins.

---

### 8. **FIRST\_VALUE and LAST\_VALUE**

```sql
-- Trick: Get the first and last value in a window
SELECT name, salary, 
       FIRST_VALUE(salary) OVER (PARTITION BY department ORDER BY salary) AS first_salary,
       LAST_VALUE(salary) OVER (PARTITION BY department ORDER BY salary ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS last_salary
FROM employees;
```

**Use when**: You need to get the first or last value in a partitioned window.

---

### 9. **Window Function with Frame Specification**

```sql
-- Trick: Use a specific window frame to limit the rows considered in window functions
SELECT name, salary, 
       SUM(salary) OVER (PARTITION BY department 
                         ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) AS salary_window
FROM employees;
```

**Use when**: You want to define a specific range of rows to perform window functions on, like the previous or next few rows.

---

### 10. **COUNT with OVER (Running Count)**

```sql
-- Trick: Count the number of employees in each department (cumulative count)
SELECT department, name, salary, 
       COUNT(*) OVER (PARTITION BY department ORDER BY salary) AS running_count
FROM employees;
```

**Use when**: You need to calculate a running count of rows, typically partitioned by a group.

---

### 11. **Window Function in Filtering (WITH HAVING)**

```sql
-- Trick: Filter based on window function results
SELECT department, name, salary, 
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
FROM employees
HAVING rank <= 3;
```

**Use when**: You need to filter rows based on the results of window functions.

---

### 12. **CUME\_DIST (Cumulative Distribution)**

```sql
-- Trick: Find cumulative distribution for salary ranks
SELECT name, salary, 
       CUME_DIST() OVER (ORDER BY salary DESC) AS cumulative_dist
FROM employees;
```

**Use when**: You need to calculate the cumulative distribution of values in your dataset.

---

### 13. **PERCENT\_RANK (Percent Rank)**

```sql
-- Trick: Calculate the percentage rank of each employee
SELECT name, salary, 
       PERCENT_RANK() OVER (ORDER BY salary DESC) AS percent_rank
FROM employees;
```

**Use when**: You want to calculate the relative rank of each row in percentage terms.

---

### 14. **Window Functions with Aggregates**

```sql
-- Trick: Use aggregate functions in window functions
SELECT department, name, salary, 
       SUM(salary) OVER (PARTITION BY department) AS department_total,
       AVG(salary) OVER (PARTITION BY department) AS department_avg
FROM employees;
```

**Use when**: You need to calculate aggregates over a specific window or partition.

---

### 15. **Window Functions with Multiple Partitions**

```sql
-- Trick: Use multiple PARTITION BY clauses to partition by multiple columns
SELECT department, job_title, name, salary, 
       RANK() OVER (PARTITION BY department, job_title ORDER BY salary DESC) AS rank
FROM employees;
```

**Use when**: You want to partition by multiple columns for more granular control.

---
