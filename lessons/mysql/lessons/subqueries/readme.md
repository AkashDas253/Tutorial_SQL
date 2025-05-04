## Subqueries in MySQL

A **subquery** is a query nested inside another query. Subqueries allow data to be fetched dynamically for use in `SELECT`, `INSERT`, `UPDATE`, or `DELETE` operations, making queries more flexible and powerful.

---

### 🔹 Inner Index

* [Types of Subqueries](#types-of-subqueries)
* [Subquery in SELECT](#subquery-in-select)
* [Subquery in WHERE](#subquery-in-where)
* [Subquery in FROM (Derived Table)](#subquery-in-from-derived-table)
* [Subquery in INSERT](#subquery-in-insert)
* [Subquery in UPDATE](#subquery-in-update)
* [Subquery in DELETE](#subquery-in-delete)
* [Correlated Subquery](#correlated-subquery)
* [Comparison Operators in Subqueries](#comparison-operators-in-subqueries)
* [Usage Scenarios](#usage-scenarios)

---

### Types of Subqueries

| Type                     | Description                            |
| ------------------------ | -------------------------------------- |
| Single-row subquery      | Returns one row with one column        |
| Multiple-row subquery    | Returns multiple rows of one column    |
| Multiple-column subquery | Returns multiple rows and columns      |
| Correlated subquery      | Refers to columns from the outer query |
| Nested subquery          | Subquery inside another subquery       |

---

### Subquery in SELECT

Used to return derived values for each row.

**Syntax:**

```sql
SELECT name, (SELECT COUNT(*) FROM orders WHERE customer_id = c.id) AS order_count
FROM customers AS c;
```

---

### Subquery in WHERE

Used to filter rows based on dynamic conditions.

**Syntax:**

```sql
SELECT name FROM employees
WHERE department_id = (SELECT id FROM departments WHERE name = 'Sales');
```

---

### Subquery in FROM (Derived Table)

Acts as a virtual table.

**Syntax:**

```sql
SELECT avg_salary FROM (
  SELECT department_id, AVG(salary) AS avg_salary FROM employees GROUP BY department_id
) AS dept_avg;
```

---

### Subquery in INSERT

Used to insert result of a `SELECT` query.

**Syntax:**

```sql
INSERT INTO archive_employees (id, name)
SELECT id, name FROM employees WHERE status = 'terminated';
```

---

### Subquery in UPDATE

Used to dynamically fetch values to update rows.

**Syntax:**

```sql
UPDATE employees
SET department_id = (
  SELECT id FROM departments WHERE name = 'HR'
)
WHERE name = 'Alice';
```

---

### Subquery in DELETE

Used to delete rows based on a dynamic condition.

**Syntax:**

```sql
DELETE FROM orders
WHERE customer_id IN (
  SELECT id FROM customers WHERE status = 'inactive'
);
```

---

### Correlated Subquery

Depends on the outer query for each row and runs repeatedly.

**Syntax:**

```sql
SELECT name FROM employees e
WHERE salary > (
  SELECT AVG(salary) FROM employees WHERE department_id = e.department_id
);
```

---

### Comparison Operators in Subqueries

| Operator     | Usage Example                                                    |
| ------------ | ---------------------------------------------------------------- |
| `=`          | `WHERE dept_id = (SELECT id FROM dept WHERE name = 'HR')`        |
| `IN`         | `WHERE id IN (SELECT emp_id FROM project)`                       |
| `ANY`        | `WHERE salary > ANY (SELECT salary FROM emp WHERE role='dev')`   |
| `ALL`        | `WHERE salary < ALL (SELECT salary FROM emp WHERE dept='HR')`    |
| `EXISTS`     | `WHERE EXISTS (SELECT * FROM bonus WHERE emp.id = bonus.emp_id)` |
| `NOT EXISTS` | `WHERE NOT EXISTS (SELECT * FROM leaves WHERE emp_id = e.id)`    |

---

### Usage Scenarios

* **Find customers who placed orders:**

  ```sql
  SELECT name FROM customers
  WHERE id IN (SELECT customer_id FROM orders);
  ```

* **List employees in departments with more than 5 employees:**

  ```sql
  SELECT name FROM employees e
  WHERE EXISTS (
    SELECT * FROM employees
    WHERE department_id = e.department_id
    GROUP BY department_id HAVING COUNT(*) > 5
  );
  ```

* **Get employees with max salary:**

  ```sql
  SELECT name FROM employees
  WHERE salary = (SELECT MAX(salary) FROM employees);
  ```

---

### Conclusion

Subqueries are vital tools for dynamic, conditional, and hierarchical queries. They increase SQL’s power by enabling you to build complex filtering and transformation logic in a readable way.

---
