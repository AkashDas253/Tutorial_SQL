# **ANSI Data Query Language (DQL)**  

DQL is a subset of SQL that is used to retrieve data from a database. The main command in DQL is `SELECT`, which allows querying, filtering, and organizing data based on conditions.

---

## **General Syntax of DQL**
```sql
SELECT [DISTINCT] column1, column2, ...
FROM table_name
[WHERE condition]
[GROUP BY column_name]
[HAVING condition]
[ORDER BY column_name [ASC | DESC]]
[LIMIT row_count OFFSET offset_value]
[FETCH {FIRST | NEXT} row_count {ROWS | ROW} ONLY];
```
- **`SELECT`**: Specifies the columns to retrieve.
- **`FROM`**: Defines the table from which to fetch data.
- **`DISTINCT`**: Removes duplicate values from the result.
- **`WHERE`**: Filters records based on conditions.
- **`GROUP BY`**: Groups records by a specified column.
- **`HAVING`**: Filters grouped data.
- **`ORDER BY`**: Sorts the query result.
- **`LIMIT` / `FETCH`**: Restricts the number of rows returned.
- **`OFFSET`**: Skips a specified number of rows.

---

## **DQL Commands with Details**

### **1. SELECT Statement**
The `SELECT` statement is used to retrieve data from a table.

| **Command**        | **Description**                        | **Example** |
|--------------------|------------------------------------|------------|
| `SELECT *`        | Retrieves all columns from a table. | `SELECT * FROM employees;` |
| `SELECT column1, column2` | Retrieves specific columns. | `SELECT name, salary FROM employees;` |

**Example Usage:**
```sql
SELECT name, age FROM employees;
```

---

### **2. SELECT DISTINCT**
Removes duplicate values from the result set.

**Example Usage:**
```sql
SELECT DISTINCT department FROM employees;
```

---

### **3. WHERE Clause**
Filters data based on conditions.

#### **Operators Used in WHERE**

| **Operator** | **Description** | **Example** |
|-------------|---------------|------------|
| `=`         | Equal to | `SELECT * FROM employees WHERE age = 30;` |
| `!=` or `<>` | Not equal to | `SELECT * FROM employees WHERE age != 30;` |
| `>`         | Greater than | `SELECT * FROM employees WHERE salary > 50000;` |
| `<`         | Less than | `SELECT * FROM employees WHERE salary < 50000;` |
| `BETWEEN`   | Range check | `SELECT * FROM employees WHERE salary BETWEEN 40000 AND 60000;` |
| `LIKE`      | Pattern matching | `SELECT * FROM employees WHERE name LIKE 'J%';` |
| `IN`        | Matches values from a list | `SELECT * FROM employees WHERE department IN ('HR', 'IT');` |

**Example Usage:**
```sql
SELECT * FROM employees WHERE department = 'Sales' AND salary > 50000;
```

---

### **4. ORDER BY Clause**
Sorts query results in **ascending (ASC, default)** or **descending (DESC)** order.

| **Command**    | **Description** | **Example** |
|---------------|---------------|------------|
| `ORDER BY column_name ASC` | Sorts results in ascending order. | `SELECT * FROM employees ORDER BY salary ASC;` |
| `ORDER BY column_name DESC` | Sorts results in descending order. | `SELECT * FROM employees ORDER BY salary DESC;` |

**Example Usage:**
```sql
SELECT * FROM employees ORDER BY name ASC;
```

---

### **5. GROUP BY Clause**
Groups rows that have the same values in a specified column.

**Example Usage:**
```sql
SELECT department, COUNT(*) FROM employees GROUP BY department;
```

---

### **6. HAVING Clause**
Filters records **after** the `GROUP BY` operation.

| **Command**    | **Description** | **Example** |
|---------------|---------------|------------|
| `HAVING condition` | Filters grouped results. | `SELECT department, AVG(salary) FROM employees GROUP BY department HAVING AVG(salary) > 50000;` |

**Example Usage:**
```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

---

### **7. LIMIT and OFFSET Clauses**
Limits the number of rows returned and specifies the starting point.

| **Clause** | **Description** | **Example** |
|-----------|---------------|------------|
| `LIMIT` | Restricts the number of rows returned. | `SELECT * FROM employees LIMIT 5;` |
| `OFFSET` | Skips a certain number of rows. | `SELECT * FROM employees LIMIT 5 OFFSET 2;` |

**Example Usage:**
```sql
SELECT * FROM employees LIMIT 10 OFFSET 5;
```

---

### **8. FETCH Clause (Alternative to LIMIT)**
More readable alternative to `LIMIT`.

| **Option** | **Description** | **Example** |
|-----------|---------------|------------|
| `FETCH FIRST n ROWS ONLY` | Returns the first `n` rows. | `SELECT * FROM employees FETCH FIRST 3 ROWS ONLY;` |
| `FETCH NEXT n ROWS ONLY` | Returns the next `n` rows after an `OFFSET`. | `SELECT * FROM employees OFFSET 5 FETCH NEXT 3 ROWS ONLY;` |

**Example Usage:**
```sql
SELECT * FROM employees FETCH FIRST 5 ROWS ONLY;
```

---

## **Subqueries in DQL**
A subquery is a query inside another query.

**Example Usage:**
```sql
SELECT name, salary FROM employees WHERE salary > (SELECT AVG(salary) FROM employees);
```

---

## **Joins in DQL**
Joins combine data from multiple tables.

| **Join Type**  | **Description** | **Example** |
|---------------|---------------|------------|
| `INNER JOIN` | Returns matching records from both tables. | `SELECT employees.name, department.name FROM employees INNER JOIN department ON employees.department_id = department.id;` |
| `LEFT JOIN`  | Returns all records from the left table and matching records from the right. | `SELECT employees.name, department.name FROM employees LEFT JOIN department ON employees.department_id = department.id;` |
| `RIGHT JOIN` | Returns all records from the right table and matching records from the left. | `SELECT employees.name, department.name FROM employees RIGHT JOIN department ON employees.department_id = department.id;` |
| `FULL JOIN`  | Returns all records from both tables. | `SELECT employees.name, department.name FROM employees FULL JOIN department ON employees.department_id = department.id;` |

---

## **Conclusion**
DQL, primarily through `SELECT`, allows querying data efficiently with filtering (`WHERE`), sorting (`ORDER BY`), grouping (`GROUP BY`), and limiting (`LIMIT` / `FETCH`). Advanced features like **subqueries and joins** enhance data retrieval.
