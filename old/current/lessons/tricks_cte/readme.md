## **Common Table Expressions (CTEs) Tricks**

### 1. **Basic CTE Syntax**

CTEs help simplify complex queries by breaking them down into more manageable parts. Here's the basic syntax:

```sql
WITH cte_name AS (
    -- CTE query here
    SELECT column1, column2
    FROM table
    WHERE condition
)
SELECT * FROM cte_name;
```

**Trick**: Use a CTE when your query has repetitive subqueries, to avoid duplicating logic.

---

### 2. **Recursive CTEs**

Recursive CTEs are used to query hierarchical data, such as organizational structures or bill-of-materials (BOM).

#### **Syntax for Recursive CTE**

```sql
WITH RECURSIVE cte_name AS (
    -- Base case: anchor member
    SELECT column1, column2 FROM table WHERE condition

    UNION ALL

    -- Recursive case: references the CTE itself
    SELECT t.column1, t.column2
    FROM table t
    JOIN cte_name cte ON t.parent_column = cte.column1
)
SELECT * FROM cte_name;
```

**Trick**: Use `UNION ALL` for recursion. Ensure a **base case** and a **recursive case** to avoid infinite loops.

**Example**: Find all subordinates under a manager in an employee table with hierarchical structure:

```sql
WITH RECURSIVE EmployeeHierarchy AS (
    SELECT employee_id, manager_id, name FROM employees WHERE manager_id IS NULL
    UNION ALL
    SELECT e.employee_id, e.manager_id, e.name
    FROM employees e
    INNER JOIN EmployeeHierarchy eh ON e.manager_id = eh.employee_id
)
SELECT * FROM EmployeeHierarchy;
```

---

### 3. **Multiple CTEs**

You can use multiple CTEs in a single query by separating them with commas. This helps in reusing complex logic multiple times within the query.

```sql
WITH cte1 AS (
    SELECT column1 FROM table1 WHERE condition1
), cte2 AS (
    SELECT column2 FROM table2 WHERE condition2
)
SELECT cte1.column1, cte2.column2
FROM cte1
JOIN cte2 ON cte1.column1 = cte2.column2;
```

**Trick**: Use multiple CTEs to break down large queries into smaller, reusable components for better readability and performance.

---

### 4. **CTE for Row Numbering**

You can use CTEs for generating row numbers, ranks, or dense ranks without affecting the main query.

```sql
WITH RowRank AS (
    SELECT column1, column2, ROW_NUMBER() OVER (ORDER BY column2 DESC) AS row_num
    FROM table
)
SELECT * FROM RowRank WHERE row_num <= 10;
```

**Trick**: Use CTEs to assign row numbers and filter data dynamically without complex subqueries.

---

### 5. **CTE with Aggregation**

CTEs can be useful for calculating complex aggregates before using them in the final SELECT statement.

```sql
WITH AggregatedData AS (
    SELECT department, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT * FROM AggregatedData WHERE avg_salary > 50000;
```

**Trick**: Use CTEs for grouping and aggregation, especially if you need to reuse the aggregate result in other parts of the query.

---

### 6. **CTE for Temporary Tables**

When working with temporary data that doesn’t require physical storage (like with temporary tables), CTEs are an efficient alternative.

```sql
WITH temp_data AS (
    SELECT column1, column2 FROM table WHERE condition
)
SELECT * FROM temp_data WHERE column1 > 100;
```

**Trick**: Use CTEs as a temporary, reusable result set within the same query, which performs better than creating and dropping temporary tables.

---

### 7. **CTE for Self Joins**

Using CTEs for self joins makes it easier to understand and maintain the query structure.

```sql
WITH EmployeeManager AS (
    SELECT employee_id, manager_id, name
    FROM employees
)
SELECT e.name AS employee, m.name AS manager
FROM EmployeeManager e
LEFT JOIN EmployeeManager m ON e.manager_id = m.employee_id;
```

**Trick**: Use CTEs for self joins, especially when joining a table to itself, to make the logic clearer and more readable.

---

### 8. **CTE for Complex Filtering**

You can use CTEs to filter or calculate intermediate results, which are then applied to the final query.

```sql
WITH FilteredData AS (
    SELECT * FROM sales WHERE sales_date > '2023-01-01'
)
SELECT product_id, SUM(amount)
FROM FilteredData
GROUP BY product_id;
```

**Trick**: Use CTEs to pre-filter data that will be used multiple times in the query, improving efficiency.

---

### 9. **CTE for Pivoting Data**

You can use CTEs in combination with `PIVOT` or `CASE` to transform data from rows into columns.

```sql
WITH SalesData AS (
    SELECT product, sales_month, amount
    FROM sales
)
SELECT product,
       SUM(CASE WHEN sales_month = 'January' THEN amount ELSE 0 END) AS January,
       SUM(CASE WHEN sales_month = 'February' THEN amount ELSE 0 END) AS February
FROM SalesData
GROUP BY product;
```

**Trick**: Use CTEs to transform data (like pivoting) before applying aggregation or filtering.

---

### 10. **CTE for Simplifying Complex Queries**

CTEs can simplify complex queries by breaking them down into logical, digestible pieces.

```sql
WITH DepartmentSalary AS (
    SELECT department_id, SUM(salary) AS total_salary
    FROM employees
    GROUP BY department_id
),
DepartmentHead AS (
    SELECT department_id, employee_id AS head_id
    FROM departments
    WHERE is_head = 1
)
SELECT d.department_id, ds.total_salary, dh.head_id
FROM DepartmentSalary ds
JOIN DepartmentHead dh ON ds.department_id = dh.department_id;
```

**Trick**: Use CTEs to break down complex business logic into smaller, more understandable parts, improving maintainability.

---

### Key Tips for Using CTEs:

* **Readability**: CTEs make queries more readable and maintainable by breaking complex logic into separate components.
* **Reuse**: Reuse logic within the same query without repeating code, making the query more efficient.
* **Performance**: While CTEs can improve readability, they don't always improve performance. For larger datasets, analyze query plans for optimization.
* **Recursion**: Recursive CTEs are ideal for hierarchical data like organizational structures or family trees.
* **Subqueries**: You can use CTEs instead of subqueries for better clarity and reusability.

---
