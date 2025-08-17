## **Data Query Language (DQL) in PostgreSQL**  

DQL is used to retrieve data from a database. The primary command in DQL is `SELECT`, which allows querying specific columns, filtering results, and performing aggregations.

---

### **1. SELECT Statement**  
The `SELECT` statement retrieves data from tables.

#### **Basic Syntax**  
```sql
SELECT column1, column2, ... FROM table_name;
```

##### **Example**  
```sql
SELECT name, salary FROM employees;
```

---

### **2. SELECT with WHERE Clause**  
Filters records based on a condition.

##### **Syntax**  
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```

##### **Example**  
```sql
SELECT name FROM employees WHERE salary > 50000;
```

##### **Operators in WHERE Clause**  
| Operator | Description | Example |
|----------|-------------|---------|
| `=` | Equals | `salary = 50000` |
| `!=` or `<>` | Not equal | `salary <> 50000` |
| `>` | Greater than | `salary > 50000` |
| `<` | Less than | `salary < 50000` |
| `BETWEEN` | Range check | `salary BETWEEN 40000 AND 60000` |
| `IN` | Matches values in a list | `dept_id IN (1, 2, 3)` |
| `LIKE` | Pattern matching | `name LIKE 'J%'` |
| `IS NULL` | Checks for NULL values | `salary IS NULL` |

---

### **3. SELECT with ORDER BY Clause**  
Sorts the result in ascending (`ASC`) or descending (`DESC`) order.

##### **Syntax**  
```sql
SELECT column1, column2 FROM table_name ORDER BY column1 ASC|DESC;
```

##### **Example**  
```sql
SELECT name, salary FROM employees ORDER BY salary DESC;
```

---

### **4. SELECT with DISTINCT Clause**  
Removes duplicate values.

##### **Syntax**  
```sql
SELECT DISTINCT column1 FROM table_name;
```

##### **Example**  
```sql
SELECT DISTINCT department FROM employees;
```

---

### **5. SELECT with LIMIT and OFFSET**  
Limits the number of rows returned.

##### **Syntax**  
```sql
SELECT column1 FROM table_name LIMIT number OFFSET number;
```

##### **Example**  
```sql
SELECT name FROM employees LIMIT 5 OFFSET 10;
```
> **Note:** `OFFSET` skips rows before returning results.

---

### **6. SELECT with GROUP BY Clause**  
Groups records based on a column and performs aggregations.

##### **Syntax**  
```sql
SELECT column, AGGREGATE_FUNCTION(column) FROM table_name GROUP BY column;
```

##### **Example**  
```sql
SELECT department, AVG(salary) FROM employees GROUP BY department;
```

##### **Common Aggregate Functions**  
| Function | Description | Example |
|----------|-------------|---------|
| `COUNT()` | Counts rows | `COUNT(*)` |
| `SUM()` | Sums column values | `SUM(salary)` |
| `AVG()` | Computes average | `AVG(salary)` |
| `MIN()` | Finds minimum | `MIN(salary)` |
| `MAX()` | Finds maximum | `MAX(salary)` |

---

### **7. SELECT with HAVING Clause**  
Filters grouped results.

##### **Syntax**  
```sql
SELECT column, AGGREGATE_FUNCTION(column) FROM table_name 
GROUP BY column HAVING condition;
```

##### **Example**  
```sql
SELECT department, AVG(salary) FROM employees 
GROUP BY department HAVING AVG(salary) > 50000;
```

---

### **8. SELECT with JOINS**  
Combines rows from multiple tables.

#### **Types of Joins**  
| Join Type | Description |
|-----------|-------------|
| `INNER JOIN` | Returns matching rows in both tables |
| `LEFT JOIN` | Returns all rows from the left table and matching rows from the right table |
| `RIGHT JOIN` | Returns all rows from the right table and matching rows from the left table |
| `FULL JOIN` | Returns all rows when there's a match in either table |

##### **Syntax**  
```sql
SELECT t1.column, t2.column FROM table1 t1 
JOIN table2 t2 ON t1.common_column = t2.common_column;
```

##### **Example**  
```sql
SELECT e.name, d.name FROM employees e 
INNER JOIN departments d ON e.dept_id = d.id;
```

---

### **9. SELECT with Subqueries**  
A subquery is a query inside another query.

##### **Syntax**  
```sql
SELECT column FROM table WHERE column = (SELECT column FROM table WHERE condition);
```

##### **Example**  
```sql
SELECT name FROM employees 
WHERE salary = (SELECT MAX(salary) FROM employees);
```

---

### **10. SELECT with Common Table Expressions (CTE)**  
CTEs improve query readability.

##### **Syntax**  
```sql
WITH cte_name AS (
    SELECT column FROM table WHERE condition
)
SELECT * FROM cte_name;
```

##### **Example**  
```sql
WITH high_salary AS (
    SELECT name, salary FROM employees WHERE salary > 50000
)
SELECT * FROM high_salary;
```

---

### **Notes**  
- **`SELECT *` is used to fetch all columns, but it’s inefficient.**  
- **Use `WHERE` before `GROUP BY`, and `HAVING` after `GROUP BY`.**  
- **Indexes improve `ORDER BY`, `WHERE`, and `JOIN` performance.**  

---
