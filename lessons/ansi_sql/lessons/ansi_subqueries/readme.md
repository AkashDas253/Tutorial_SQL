## ANSI Subqueries

A **subquery** is a query nested inside another query. Subqueries allow for more complex querying by embedding one SQL query within another to retrieve intermediate results that can be used by the outer query. Subqueries can appear in various places, including the `SELECT`, `FROM`, `WHERE`, and `HAVING` clauses.

### Types of Subqueries

| **Subquery Type**         | **Description**                                                                                           | **Example**                                                       |  
|---------------------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
| **Scalar Subquery**        | A subquery that returns a single value (one column and one row). It is used in places where a single value is expected, such as in the `WHERE` clause.              | `SELECT name FROM employees WHERE id = (SELECT MAX(id) FROM employees);`    |  
| **Column Subquery**        | A subquery that returns a set of values (one column and multiple rows). It is used in comparisons with a column in the outer query. | `SELECT name FROM employees WHERE department_id IN (SELECT department_id FROM departments WHERE location = 'New York');` |  
| **Row Subquery**           | A subquery that returns a single row but can have multiple columns. It is typically used in comparisons with a row from the outer query. | `SELECT name FROM employees WHERE (department_id, salary) = (SELECT department_id, salary FROM employees WHERE id = 3);`  |  
| **Table Subquery**         | A subquery that returns multiple rows and columns (a table-like result). It is used in the `FROM` clause, creating a derived table that can be joined with other tables. | `SELECT avg_salary FROM (SELECT department_id, AVG(salary) AS avg_salary FROM employees GROUP BY department_id) AS department_avg;` |  
| **Correlated Subquery**    | A subquery that references a column from the outer query. It is executed once for each row processed by the outer query, allowing for row-by-row comparison. | `SELECT name FROM employees e WHERE salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);`  |  

---

### **Scalar Subquery**

A **scalar subquery** returns exactly one value (one column, one row). It is commonly used in comparison operations where the result of the subquery is compared to a column in the outer query.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                       |  
|------------------------|---------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
| `SELECT`               | The subquery that retrieves a single value (one row, one column).                                        | `SELECT name FROM employees WHERE id = (SELECT MAX(id) FROM employees);` |  

**Usage Example**:  
```sql
SELECT name
FROM employees
WHERE id = (SELECT MAX(id) FROM employees);
```

---

### **Column Subquery**

A **column subquery** returns multiple rows but only one column. It is often used with the `IN` operator to check if a column value exists in the list of values returned by the subquery.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                       |  
|------------------------|---------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
| `IN`                   | The operator used to match a column value against a set of values returned by a subquery.               | `SELECT name FROM employees WHERE department_id IN (SELECT department_id FROM departments WHERE location = 'New York');`  |  

**Usage Example**:  
```sql
SELECT name
FROM employees
WHERE department_id IN (SELECT department_id FROM departments WHERE location = 'New York');
```

---

### **Row Subquery**

A **row subquery** returns a single row but may contain multiple columns. It is typically used in comparisons where the outer query's row is compared to the result of the subquery.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                       |  
|------------------------|---------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
| `=`, `>`, `<`           | Comparison operators used to compare rows in a subquery.                                                | `SELECT name FROM employees WHERE (department_id, salary) = (SELECT department_id, salary FROM employees WHERE id = 3);` |  

**Usage Example**:  
```sql
SELECT name
FROM employees
WHERE (department_id, salary) = (SELECT department_id, salary FROM employees WHERE id = 3);
```

---

### **Table Subquery**

A **table subquery** returns multiple rows and multiple columns, essentially producing a derived table. It is used in the `FROM` clause to create a temporary table that can be joined or queried further.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                       |  
|------------------------|---------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
| `FROM`                 | The clause in which a subquery returns a derived table that can be used as a source for further queries. | `SELECT avg_salary FROM (SELECT department_id, AVG(salary) AS avg_salary FROM employees GROUP BY department_id) AS department_avg;` |  

**Usage Example**:  
```sql
SELECT avg_salary
FROM (
  SELECT department_id, AVG(salary) AS avg_salary
  FROM employees
  GROUP BY department_id
) AS department_avg;
```

---

### **Correlated Subquery**

A **correlated subquery** is a subquery that depends on the outer query. It references columns from the outer query, and for each row processed by the outer query, the subquery is executed. This results in row-by-row comparison.

#### Syntax Overview

| **Clause**             | **Description**                                                                                         | **Example**                                                       |  
|------------------------|---------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
| `WHERE`                | The correlated subquery uses a column from the outer query in its comparison.                            | `SELECT name FROM employees e WHERE salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);` |  

**Usage Example**:  
```sql
SELECT name
FROM employees e
WHERE salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);
```

---

### Conclusion

ANSI subqueries are powerful tools in SQL that enable complex queries by embedding one query inside another. The various types of subqueries—**scalar**, **column**, **row**, **table**, and **correlated**—offer flexibility in retrieving and manipulating data from multiple tables. Subqueries can be used in `SELECT`, `FROM`, `WHERE`, and other clauses, allowing for dynamic querying based on intermediate results.
