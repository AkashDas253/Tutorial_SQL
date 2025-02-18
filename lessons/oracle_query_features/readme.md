Here’s a comprehensive note on **Query Features** in Oracle SQL, covering Joins, Subqueries, Set Operations, Group By Features, and Analytical Functions, including their syntax and usage examples.

## Query Features in Oracle SQL

### 1. **Joins**

#### 1.1 **Inner Joins**
An inner join returns only the rows that have matching values in both tables.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Returns matching rows from both tables based on a condition   | `SELECT * FROM table1 INNER JOIN table2 ON table1.id = table2.id;` |

#### Example:
```sql
SELECT employees.name, departments.name
FROM employees
INNER JOIN departments ON employees.department_id = departments.id;
```

#### 1.2 **Outer Joins**

Outer joins return all rows from one table and the matching rows from the second table. If no match is found, the result will contain NULL for columns from the second table.

| **Type**     | **Description**                                             | **Syntax Example**                                              |
|--------------|-------------------------------------------------------------|-----------------------------------------------------------------|
| **Left Join**| Returns all rows from the left table and matched rows from the right table. If no match, NULLs for right table columns | `SELECT * FROM table1 LEFT JOIN table2 ON table1.id = table2.id;` |
| **Right Join**| Returns all rows from the right table and matched rows from the left table. If no match, NULLs for left table columns | `SELECT * FROM table1 RIGHT JOIN table2 ON table1.id = table2.id;` |
| **Full Join**| Returns all rows when there is a match in either left or right table. If no match, NULLs for missing side | `SELECT * FROM table1 FULL OUTER JOIN table2 ON table1.id = table2.id;` |

#### Example:
```sql
SELECT employees.name, departments.name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.id;
```

#### 1.3 **Cross Joins**
A cross join returns the Cartesian product of two tables, i.e., each row from the first table is combined with all rows from the second table.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Returns all possible combinations of rows from both tables    | `SELECT * FROM table1 CROSS JOIN table2;`                      |

#### Example:
```sql
SELECT employees.name, departments.name
FROM employees
CROSS JOIN departments;
```

#### 1.4 **Self Joins**
A self join is a join where a table is joined with itself, often used to compare rows within the same table.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Joins a table with itself to compare rows                     | `SELECT A.name, B.name FROM employees A, employees B WHERE A.manager_id = B.id;` |

#### Example:
```sql
SELECT A.name AS Employee, B.name AS Manager
FROM employees A, employees B
WHERE A.manager_id = B.id;
```

---

### 2. **Subqueries**

#### 2.1 **Single-Row Subqueries**
A single-row subquery returns only one row with one or more columns, and the result is used in the parent query.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Returns a single value to be used in the parent query         | `SELECT * FROM employees WHERE salary = (SELECT MAX(salary) FROM employees);` |

#### Example:
```sql
SELECT name, salary
FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);
```

#### 2.2 **Multi-Row Subqueries**
A multi-row subquery returns multiple rows and is used with operators like `IN`, `ANY`, or `ALL`.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Returns multiple rows to be compared in the parent query      | `SELECT * FROM employees WHERE department_id IN (SELECT id FROM departments WHERE location = 'New York');` |

#### Example:
```sql
SELECT name, salary
FROM employees
WHERE department_id IN (SELECT id FROM departments WHERE location = 'New York');
```

#### 2.3 **Correlated Subqueries**
A correlated subquery is a subquery that references a column from the outer query. It is executed once for each row processed by the outer query.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | References outer query columns to calculate the result        | `SELECT name FROM employees e WHERE salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);` |

#### Example:
```sql
SELECT name
FROM employees e
WHERE salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);
```

#### 2.4 **Inline Views**
An inline view is a subquery that appears in the `FROM` clause, allowing it to be treated as a table.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Subquery in the `FROM` clause to act as a virtual table       | `SELECT name FROM (SELECT name, salary FROM employees WHERE department_id = 1) AS emp WHERE salary > 5000;` |

#### Example:
```sql
SELECT name
FROM (SELECT name, salary FROM employees WHERE department_id = 1) AS emp
WHERE salary > 5000;
```

---

### 3. **Set Operations**

#### 3.1 **`UNION` and `UNION ALL`**
The `UNION` operator combines the results of two queries, removing duplicates, whereas `UNION ALL` includes all results, including duplicates.

| **Operator**           | **Description**                                               | **Syntax Example**                                             |
|------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **`UNION`**             | Combines results of two queries, removing duplicates          | `SELECT column FROM table1 UNION SELECT column FROM table2;`    |
| **`UNION ALL`**         | Combines results, including duplicates                        | `SELECT column FROM table1 UNION ALL SELECT column FROM table2;` |

#### Example:
```sql
SELECT name FROM employees
UNION
SELECT name FROM contractors;
```

#### 3.2 **`INTERSECT`**
The `INTERSECT` operator returns the common rows between two queries.

| **Operator**           | **Description**                                               | **Syntax Example**                                             |
|------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **`INTERSECT`**         | Returns common rows between two queries                       | `SELECT column FROM table1 INTERSECT SELECT column FROM table2;` |

#### Example:
```sql
SELECT name FROM employees
INTERSECT
SELECT name FROM contractors;
```

#### 3.3 **`MINUS`**
The `MINUS` operator returns the rows from the first query that are not present in the second query.

| **Operator**           | **Description**                                               | **Syntax Example**                                             |
|------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **`MINUS`**             | Returns rows from the first query that aren't in the second   | `SELECT column FROM table1 MINUS SELECT column FROM table2;`    |

#### Example:
```sql
SELECT name FROM employees
MINUS
SELECT name FROM contractors;
```

---

### 4. **Group By Features**

#### 4.1 **`GROUP BY`**
The `GROUP BY` statement groups rows that have the same values into summary rows, such as finding the sum or average.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Groups rows and applies aggregate functions                  | `SELECT department_id, AVG(salary) FROM employees GROUP BY department_id;` |

#### Example:
```sql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id;
```

#### 4.2 **`HAVING`**
The `HAVING` clause filters the results of a `GROUP BY` query based on conditions for aggregated data.

| **Property**            | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Purpose**              | Filters groups based on a condition for aggregate results      | `SELECT department_id, AVG(salary) FROM employees GROUP BY department_id HAVING AVG(salary) > 5000;` |

#### Example:
```sql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 5000;
```

#### 4.3 **Rollups and Cubes**
Rollups and cubes are used to generate subtotals and grand totals.

| **Feature**             | **Description**                                               | **Syntax Example**                                             |
|-------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Rollup**              | Generates subtotals and grand total                           | `SELECT department_id, SUM(salary) FROM employees GROUP BY ROLLUP(department_id);` |
| **Cube**                | Generates subtotals for all combinations of grouping columns  | `SELECT department_id, job_id, SUM(salary) FROM employees GROUP BY CUBE(department_id, job_id);` |

#### Example:
```sql
SELECT department_id, SUM(salary)
FROM employees
GROUP BY ROLLUP(department_id);
```

---

### 5. **Analytical Functions**

#### 5.1 **Ranking Functions**
Ranking functions assign a rank to each row in a result set, based on a specified order.

| **Function**             | **Description**                                               | **Syntax Example**                                             |
|--------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **RANK()**               | Assigns a rank with gaps between equal values                 | `SELECT name, salary, RANK() OVER (ORDER BY salary DESC) FROM employees;` |
| **DENSE_RANK()**         | Assigns ranks without gaps between equal values               | `SELECT name, salary, DENSE_RANK() OVER (ORDER BY salary DESC) FROM employees;` |
| **ROW_NUMBER()**         | Assigns a unique number to each row                           | `SELECT name, salary, ROW_NUMBER() OVER (ORDER BY salary DESC) FROM employees;` |

#### Example:
```sql
SELECT name, salary, RANK() OVER (ORDER BY salary DESC) AS rank
FROM employees;
```

#### 5.2 **Aggregate Functions**
Analytical aggregate functions like `SUM`, `AVG`, `MAX`, `MIN`, `COUNT` perform calculations across a range of rows.

| **Function**             | **Description**                                               | **Syntax Example**                                             |
|--------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **SUM()**                | Calculates the sum of values                                  | `SELECT SUM(salary) OVER (PARTITION BY department_id) FROM employees;` |
| **AVG()**                | Calculates the average of values                              | `SELECT AVG(salary) OVER (PARTITION BY department_id) FROM employees;` |

#### Example:
```sql
SELECT department_id, AVG(salary) OVER (PARTITION BY department_id)
FROM employees;
```

#### 5.3 **Windowing Functions**
Windowing functions allow calculations over a set of rows related to the current row.

| **Function**             | **Description**                                               | **Syntax Example**                                             |
|--------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **OVER()**               | Defines the window for a function                              | `SELECT salary, AVG(salary) OVER (PARTITION BY department_id ORDER BY salary) FROM employees;` |

#### Example:
```sql
SELECT name, salary, AVG(salary) OVER (PARTITION BY department_id ORDER BY salary) AS avg_salary
FROM employees;
```

---
