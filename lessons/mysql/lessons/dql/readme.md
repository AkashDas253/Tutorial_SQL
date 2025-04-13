## Data Query Language (DQL) in MySQL

---

### ▪️ Overview

**Data Query Language (DQL)** in MySQL refers to the SQL commands used to **retrieve data** from a database. The primary focus of DQL is **querying** databases without modifying any data. It provides a powerful mechanism for extracting, filtering, sorting, and analyzing data.

The most commonly used DQL command in MySQL is `SELECT`.

---

### ▪️ Key DQL Command

| Command   | Purpose                                      |
|-----------|----------------------------------------------|
| `SELECT`  | Retrieve data from one or more tables        |

---

### ▪️ Syntax and Usage

#### 🔹 `SELECT`
```sql
-- Basic Select
SELECT column1, column2 FROM table_name;

-- Select all columns
SELECT * FROM table_name;

-- Select with WHERE condition
SELECT column1, column2 FROM table_name WHERE condition;

-- Select with ORDER BY
SELECT column1, column2 FROM table_name ORDER BY column1 DESC;

-- Select with LIMIT
SELECT column1, column2 FROM table_name LIMIT 10;

-- Select distinct (no duplicates)
SELECT DISTINCT column1 FROM table_name;

-- Aggregate Functions with GROUP BY
SELECT COUNT(*), AVG(price) FROM products GROUP BY category;

-- Select with JOIN
SELECT a.column1, b.column2 FROM table1 a
JOIN table2 b ON a.id = b.id;

-- Select with Subquery
SELECT column1 FROM table_name WHERE column2 = (SELECT column2 FROM another_table);
```

---

### ▪️ Clauses and Modifiers in DQL

| Clause           | Purpose                                           |
|------------------|---------------------------------------------------|
| `WHERE`          | Filters the result set based on conditions         |
| `ORDER BY`       | Sorts the result set based on one or more columns |
| `GROUP BY`       | Groups rows that have the same values into summary |
| `HAVING`         | Filters the result after the `GROUP BY` clause    |
| `DISTINCT`       | Removes duplicate rows from the result set        |
| `LIMIT`          | Limits the number of rows returned                |
| `OFFSET`         | Specifies the starting point for the result set   |
| `JOIN`           | Combines rows from two or more tables based on a related column |
| `ON`             | Specifies the condition for `JOIN`                |
| `IN`             | Filters results based on a list of values         |
| `BETWEEN`        | Selects values within a specified range           |
| `LIKE`           | Filters results based on a pattern match          |
| `IS NULL`        | Filters results based on null values              |

---

### ▪️ Usage Scenarios

| Scenario                                      | DQL Command Used          |
|-----------------------------------------------|---------------------------|
| Retrieve customer details                     | `SELECT`                  |
| Get all orders placed by a specific user      | `SELECT` with `WHERE`     |
| Retrieve product prices sorted by category    | `SELECT` with `ORDER BY`  |
| Get the average salary by department          | `SELECT` with `GROUP BY`  |
| Get all distinct values from a column         | `SELECT DISTINCT`         |
| Retrieve a subset of rows (pagination)        | `SELECT` with `LIMIT`     |

---

### ▪️ Aggregation in DQL

| Function          | Description                                      |
|-------------------|--------------------------------------------------|
| `COUNT()`         | Returns the number of rows                      |
| `SUM()`           | Returns the sum of values in a column           |
| `AVG()`           | Returns the average of values in a column       |
| `MIN()`           | Returns the smallest value in a column          |
| `MAX()`           | Returns the largest value in a column           |

Example:
```sql
SELECT AVG(price) FROM products;
```

---

### ▪️ JOINs in DQL

| Type              | Description                                      |
|-------------------|--------------------------------------------------|
| `INNER JOIN`      | Returns only the rows where there is a match in both tables |
| `LEFT JOIN`       | Returns all rows from the left table, and matched rows from the right table |
| `RIGHT JOIN`      | Returns all rows from the right table, and matched rows from the left table |
| `FULL OUTER JOIN` | Combines the result of both `LEFT JOIN` and `RIGHT JOIN` |
| `CROSS JOIN`      | Returns the Cartesian product of both tables (every row in the first table is combined with every row in the second table) |
| `SELF JOIN`       | Joins the table with itself                      |

Example:
```sql
SELECT a.name, b.salary
FROM employees a
INNER JOIN salaries b ON a.id = b.employee_id;
```

---

### ▪️ Subqueries in DQL

- **Single-row Subquery**: Returns a single value.
- **Multi-row Subquery**: Returns multiple values.
- **Correlated Subquery**: References a column from the outer query.

Example:
```sql
-- Single-row Subquery
SELECT * FROM employees WHERE department_id = (SELECT department_id FROM departments WHERE name = 'HR');

-- Correlated Subquery
SELECT employee_id, salary FROM employees e WHERE e.salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);
```

---

### ▪️ DQL Performance Considerations

| Best Practice                          | Benefit                                      |
|----------------------------------------|----------------------------------------------|
| Use indexes on columns used in `WHERE`, `ORDER BY`, and `JOIN` | Improves query performance                   |
| Avoid `SELECT *`                       | Reduces unnecessary data retrieval           |
| Use `LIMIT` for pagination             | Reduces the amount of data fetched at once   |
| Optimize JOINs with proper indexing    | Speeds up join operations                    |

---

### ▪️ DQL vs DML vs DDL

| Feature         | DQL                               | DML                             | DDL                             |
|-----------------|-----------------------------------|---------------------------------|----------------------------------|
| Purpose         | Retrieve data                    | Modify data                     | Define schema                   |
| Transactional   | No                                | Yes                             | No                               |
| Rollback Support| No                                | Yes                             | No                               |
| Affects         | Data (displayed)                  | Data (modified)                 | Structure (database/table)       |

---
