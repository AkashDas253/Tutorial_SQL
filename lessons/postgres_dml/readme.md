## **Data Manipulation Language (DML) in PostgreSQL**  

DML consists of SQL commands that manipulate data stored in database tables. It includes `INSERT`, `UPDATE`, `DELETE`, and `SELECT` (when used for data retrieval).  

### **1. INSERT Statement**  
The `INSERT` statement is used to add new records to a table.  

#### **Syntax**  
```sql
INSERT INTO table_name (column1, column2, ...) 
VALUES (value1, value2, ...);
```

#### **Options**  
| Option               | Description                                         | Example |
|----------------------|-----------------------------------------------------|---------|
| **INSERT INTO**      | Specifies the target table                         | `INSERT INTO employees (id, name, salary) VALUES (1, 'Alice', 50000);` |
| **VALUES**           | Defines the values to be inserted                   | `INSERT INTO products (id, name) VALUES (101, 'Laptop');` |
| **DEFAULT**          | Inserts the default value for a column              | `INSERT INTO employees (id, name, salary) VALUES (2, 'Bob', DEFAULT);` |
| **RETURNING**        | Returns inserted values                             | `INSERT INTO employees (name) VALUES ('Charlie') RETURNING id;` |
| **INSERT INTO ... SELECT** | Inserts data from another table             | `INSERT INTO archived_orders SELECT * FROM orders WHERE order_date < '2024-01-01';` |

---

### **2. UPDATE Statement**  
The `UPDATE` statement modifies existing records in a table.  

#### **Syntax**  
```sql
UPDATE table_name 
SET column1 = value1, column2 = value2 
WHERE condition;
```

#### **Options**  
| Option               | Description                                         | Example |
|----------------------|-----------------------------------------------------|---------|
| **SET**             | Specifies the columns to update                      | `UPDATE employees SET salary = 60000 WHERE id = 1;` |
| **WHERE**           | Filters which rows to update                         | `UPDATE products SET price = price * 1.1 WHERE category = 'Electronics';` |
| **RETURNING**       | Returns updated values                              | `UPDATE employees SET salary = 55000 WHERE id = 1 RETURNING *;` |

---

### **3. DELETE Statement**  
The `DELETE` statement removes records from a table.  

#### **Syntax**  
```sql
DELETE FROM table_name 
WHERE condition;
```

#### **Options**  
| Option               | Description                                         | Example |
|----------------------|-----------------------------------------------------|---------|
| **WHERE**           | Filters which rows to delete                        | `DELETE FROM employees WHERE id = 5;` |
| **DELETE ALL ROWS** | Deletes all rows without deleting the table        | `DELETE FROM employees;` |
| **RETURNING**       | Returns deleted values                              | `DELETE FROM employees WHERE id = 1 RETURNING *;` |

> **Note:** To remove all rows from a table and reset auto-increment counters, use `TRUNCATE` instead of `DELETE`.  

---

### **4. SELECT Statement (for Data Retrieval)**  
The `SELECT` statement retrieves data from tables.  

#### **Syntax**  
```sql
SELECT column1, column2 
FROM table_name 
WHERE condition;
```

#### **Options**  
| Option                | Description                                         | Example |
|-----------------------|-----------------------------------------------------|---------|
| **DISTINCT**         | Removes duplicate values                            | `SELECT DISTINCT department FROM employees;` |
| **ORDER BY**        | Sorts query results                                  | `SELECT * FROM employees ORDER BY salary DESC;` |
| **GROUP BY**        | Groups results for aggregation                       | `SELECT department, COUNT(*) FROM employees GROUP BY department;` |
| **HAVING**          | Filters grouped data                                 | `SELECT department, AVG(salary) FROM employees GROUP BY department HAVING AVG(salary) > 50000;` |
| **LIMIT**/**OFFSET** | Limits or paginates results                         | `SELECT * FROM employees LIMIT 10 OFFSET 5;` |

---

### **5. Transaction Control with DML**  
Transactions ensure data integrity and consistency.  

#### **Syntax**  
```sql
BEGIN;
UPDATE employees SET salary = 70000 WHERE id = 3;
DELETE FROM employees WHERE id = 4;
COMMIT;
```

#### **Options**  
| Command  | Description                                       | Example |
|----------|---------------------------------------------------|---------|
| **BEGIN**  | Starts a transaction                           | `BEGIN;` |
| **COMMIT** | Saves changes permanently                     | `COMMIT;` |
| **ROLLBACK** | Reverts changes if an error occurs        | `ROLLBACK;` |

---

### **6. Examples of DML Usage**  

#### **Insert and Retrieve Data**  
```sql
INSERT INTO employees (id, name, salary) VALUES (1, 'Alice', 50000);
SELECT * FROM employees;
```

#### **Update Data**  
```sql
UPDATE employees SET salary = salary + 5000 WHERE id = 1;
SELECT * FROM employees WHERE id = 1;
```

#### **Delete Data**  
```sql
DELETE FROM employees WHERE id = 1;
SELECT * FROM employees;
```

#### **Transaction Example**  
```sql
BEGIN;
UPDATE employees SET salary = salary * 1.1 WHERE department = 'IT';
ROLLBACK;  -- Cancels the update
```

---

### **Notes**  
- **Transactions** are important for maintaining database integrity.  
- **The `WHERE` clause** is crucial to avoid accidental updates or deletions of all records.  
- **`RETURNING`** is useful to retrieve affected rows immediately after an `INSERT`, `UPDATE`, or `DELETE`.  

---
