## 🛠️ **Data Manipulation Tricks in SQL**

### 1. **INSERT INTO with SELECT**

```sql
-- Trick: Insert data from one table into another
INSERT INTO new_table (col1, col2)
SELECT col1, col2 FROM old_table
WHERE condition;
```

**Use when**: You want to copy data between tables or insert specific data based on a condition.

---

### 2. **UPDATE with JOIN**

```sql
-- Trick: Update data using another table
UPDATE employees e
JOIN departments d ON e.dept_id = d.id
SET e.salary = e.salary * 1.1
WHERE d.name = 'Sales';
```

**Use when**: You need to update one table based on matching data from another table.

---

### 3. **DELETE with JOIN**

```sql
-- Trick: Delete records based on another table’s data
DELETE e FROM employees e
JOIN departments d ON e.dept_id = d.id
WHERE d.name = 'HR';
```

**Use when**: You need to delete rows based on related data from other tables.

---

### 4. **INSERT INTO with Multiple Rows**

```sql
-- Trick: Insert multiple rows in one query
INSERT INTO products (name, price)
VALUES ('Product A', 10),
       ('Product B', 15),
       ('Product C', 20);
```

**Use when**: You need to insert several rows at once, saving execution time.

---

### 5. **UPSERT with INSERT … ON DUPLICATE KEY UPDATE (MySQL)**

```sql
-- Trick: Insert or update in MySQL (No need to check existence first)
INSERT INTO users (email, name) 
VALUES ('user@example.com', 'John Doe') 
ON DUPLICATE KEY UPDATE name = 'John Doe';
```

**Use when**: You need to either insert new records or update existing ones in a single query.

---

### 6. **MERGE Statement (SQL Server, Oracle)**

```sql
-- Trick: Efficiently perform insert, update, or delete in one statement
MERGE INTO employees e
USING temp_employees t ON e.id = t.id
WHEN MATCHED THEN
  UPDATE SET e.salary = t.salary
WHEN NOT MATCHED THEN
  INSERT (id, name, salary) VALUES (t.id, t.name, t.salary);
```

**Use when**: You need to merge data from two tables, performing insert, update, or delete based on matching conditions.

---

### 7. **Using Subqueries in Data Manipulation**

```sql
-- Trick: Use subquery to fetch data for INSERT or UPDATE
UPDATE employees
SET salary = (SELECT AVG(salary) FROM employees WHERE department = 'Sales')
WHERE department = 'HR';
```

**Use when**: You want to use aggregated or specific data from another query in your data manipulation.

---

### 8. **DELETE with a Condition on Aggregated Data**

```sql
-- Trick: Delete employees who haven’t met a minimum order requirement
DELETE FROM employees
WHERE id NOT IN (
  SELECT employee_id FROM orders
  GROUP BY employee_id
  HAVING COUNT(*) > 10
);
```

**Use when**: You need to delete records based on aggregate data from a related table.

---

### 9. **Transactional Integrity with COMMIT/ROLLBACK**

```sql
-- Trick: Ensure atomicity for data manipulations
START TRANSACTION;

UPDATE employees SET salary = salary * 1.1 WHERE department = 'Marketing';

-- If all good
COMMIT;

-- If something goes wrong
ROLLBACK;
```

**Use when**: You want to group multiple data manipulation queries to commit all at once or roll back if something goes wrong.

---

### 10. **Conditional UPDATE with CASE**

```sql
-- Trick: Conditional update using CASE
UPDATE employees
SET salary = CASE
                WHEN years_at_company > 5 THEN salary * 1.2
                ELSE salary * 1.1
             END;
```

**Use when**: You want to apply conditional logic to updates.

---

### 11. **Truncate Table for Quick Data Deletion**

```sql
-- Trick: Remove all rows quickly (without logging individual row deletions)
TRUNCATE TABLE employees;
```

**Use when**: You need to delete all data from a table quickly, without deleting the table structure.

---

### 12. **Batch Data Insertion with Common Table Expressions (CTEs)**

```sql
-- Trick: Insert data in batches using CTEs
WITH new_employees AS (
  SELECT 'Alice' AS name, 40000 AS salary
  UNION ALL
  SELECT 'Bob', 45000
)
INSERT INTO employees (name, salary)
SELECT name, salary FROM new_employees;
```

**Use when**: You want to insert data in a structured, modular way.

---

### 13. **Handling NULLs with COALESCE or IFNULL**

```sql
-- Trick: Replace NULL with a default value
SELECT name, COALESCE(phone, 'No Phone') AS contact
FROM employees;
```

**Use when**: You want to substitute `NULL` values with meaningful defaults during data retrieval or updates.

---

### 14. **Handling Duplicate Data in INSERT**

```sql
-- Trick: Avoid inserting duplicate data (MySQL example)
INSERT IGNORE INTO users (email, name)
VALUES ('user@example.com', 'Jane Doe');
```

**Use when**: You want to ensure no duplicates are inserted without explicitly checking for them.

---

### 15. **Batch Updates with WHERE IN**

```sql
-- Trick: Update multiple records in a single query
UPDATE employees
SET salary = salary * 1.05
WHERE department IN ('Marketing', 'Sales');
```

**Use when**: You want to apply an update to a specific set of records.

---
