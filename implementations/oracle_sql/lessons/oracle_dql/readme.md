## **Data Query Language (DQL) in Oracle SQL**  

DQL (Data Query Language) consists of commands used to **retrieve data** from a database. The primary command in DQL is **`SELECT`**, which fetches data from one or more tables based on specified conditions.  

---

## **1. DQL Command: `SELECT`**  

| **Command**  | **Description** |
|-------------|---------------|
| `SELECT`    | Retrieves data from a table based on specified conditions. |

---

## **2. Basic `SELECT` Syntax**  

```sql
SELECT column1, column2, ... FROM table_name WHERE condition;
```

---

## **3. `SELECT` Features and Usage**  

### **3.1 Retrieving All Columns**  
- To fetch all columns from a table, use `*`.  

```sql
SELECT * FROM employees;
```

### **3.2 Selecting Specific Columns**  
- Retrieves only selected columns.  

```sql
SELECT first_name, last_name, salary FROM employees;
```

### **3.3 Using `WHERE` Clause**  
- Filters records based on a condition.  

```sql
SELECT first_name, salary FROM employees WHERE salary > 5000;
```

### **3.4 Using `ORDER BY` for Sorting**  
- Sorts results in ascending (`ASC`) or descending (`DESC`) order.  

```sql
SELECT first_name, salary FROM employees ORDER BY salary DESC;
```

### **3.5 Using `DISTINCT` to Remove Duplicates**  
- Returns unique values from a column.  

```sql
SELECT DISTINCT department_id FROM employees;
```

### **3.6 Using `LIMIT` (or `FETCH` in Oracle 12c+)**  
- Limits the number of rows returned.  

```sql
SELECT first_name, salary FROM employees FETCH FIRST 5 ROWS ONLY;
```

### **3.7 Using `GROUP BY` for Aggregation**  
- Groups rows and applies aggregate functions (`SUM`, `AVG`, `COUNT`, etc.).  

```sql
SELECT department_id, AVG(salary) FROM employees GROUP BY department_id;
```

### **3.8 Using `HAVING` for Filtered Aggregation**  
- Filters grouped results using conditions on aggregate functions.  

```sql
SELECT department_id, COUNT(*) FROM employees GROUP BY department_id HAVING COUNT(*) > 5;
```

### **3.9 Using `JOIN` to Combine Tables**  
- Combines records from multiple tables based on a common column.  

```sql
SELECT e.first_name, d.department_name 
FROM employees e 
JOIN departments d ON e.department_id = d.department_id;
```

### **3.10 Using Subqueries**  
- Nested queries to fetch data dynamically.  

```sql
SELECT first_name, salary FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);
```

---

## **4. Summary of `SELECT` Features**  

| **Feature** | **Usage** |
|------------|---------|
| `*` | Select all columns |
| `WHERE` | Apply conditions to filter results |
| `ORDER BY` | Sort results in ascending or descending order |
| `DISTINCT` | Retrieve unique values |
| `FETCH` | Limit the number of rows returned |
| `GROUP BY` | Group results and use aggregate functions |
| `HAVING` | Filter grouped results |
| `JOIN` | Combine tables |
| `Subqueries` | Use queries inside other queries |
