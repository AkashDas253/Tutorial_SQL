# **Data Manipulation Language (DML) in PostgreSQL**  

## **Overview**  
Data Manipulation Language (DML) in PostgreSQL consists of SQL statements used to **retrieve, insert, update, and delete data** in database tables.

---

## **1. Insert Data**  
| Action | Command |
|--------|---------|
| Insert Single Row | `INSERT INTO table_name (column1, column2) VALUES (value1, value2);` |
| Insert Multiple Rows | `INSERT INTO table_name (column1, column2) VALUES (value1, value2), (value3, value4);` |
| Insert from Another Table | `INSERT INTO table_name (column1, column2) SELECT column1, column2 FROM another_table;` |
| Insert with Default Values | `INSERT INTO table_name DEFAULT VALUES;` |
| Insert and Return Inserted Row | `INSERT INTO table_name (column1, column2) VALUES (value1, value2) RETURNING *;` |

#### **Example**
```sql
INSERT INTO employees (id, name, salary) VALUES (1, 'Alice', 50000);
```

---

## **2. Update Data**  
| Action | Command |
|--------|---------|
| Update Specific Rows | `UPDATE table_name SET column1 = value WHERE condition;` |
| Update Multiple Columns | `UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;` |
| Update All Rows | `UPDATE table_name SET column1 = value;` |
| Update and Return Affected Rows | `UPDATE table_name SET column1 = value WHERE condition RETURNING *;` |

#### **Example**
```sql
UPDATE employees SET salary = 60000 WHERE id = 1;
```

---

## **3. Delete Data**  
| Action | Command |
|--------|---------|
| Delete Specific Rows | `DELETE FROM table_name WHERE condition;` |
| Delete All Rows | `DELETE FROM table_name;` (without `WHERE`) |
| Delete and Return Deleted Rows | `DELETE FROM table_name WHERE condition RETURNING *;` |
| Truncate Table (Faster) | `TRUNCATE TABLE table_name;` |

#### **Example**
```sql
DELETE FROM employees WHERE id = 1;
```

---

## **4. Select Data**  
| Action | Command |
|--------|---------|
| Select All Columns | `SELECT * FROM table_name;` |
| Select Specific Columns | `SELECT column1, column2 FROM table_name;` |
| Select with Condition | `SELECT * FROM table_name WHERE condition;` |
| Select Distinct Values | `SELECT DISTINCT column FROM table_name;` |
| Select with Sorting | `SELECT * FROM table_name ORDER BY column ASC/DESC;` |
| Select with Limit | `SELECT * FROM table_name LIMIT n;` |
| Select with Offset | `SELECT * FROM table_name OFFSET n;` |

#### **Example**
```sql
SELECT name, salary FROM employees WHERE salary > 50000 ORDER BY salary DESC;
```

---

## **5. Joins**  
| Type | Command Example |
|------|----------------|
| Inner Join | `SELECT * FROM t1 INNER JOIN t2 ON t1.id = t2.id;` |
| Left Join | `SELECT * FROM t1 LEFT JOIN t2 ON t1.id = t2.id;` |
| Right Join | `SELECT * FROM t1 RIGHT JOIN t2 ON t1.id = t2.id;` |
| Full Join | `SELECT * FROM t1 FULL JOIN t2 ON t1.id = t2.id;` |

---

## **6. Aggregate Functions**  
| Function | Usage |
|----------|-------|
| `COUNT(*)` | `SELECT COUNT(*) FROM table_name;` |
| `SUM(column)` | `SELECT SUM(column) FROM table_name;` |
| `AVG(column)` | `SELECT AVG(column) FROM table_name;` |
| `MIN(column)` | `SELECT MIN(column) FROM table_name;` |
| `MAX(column)` | `SELECT MAX(column) FROM table_name;` |

#### **Example**
```sql
SELECT department, AVG(salary) FROM employees GROUP BY department;
```

---

## **7. RETURNING Clause**  
| **Statement** | **Description** |
|--------------|---------------|
| `INSERT INTO table_name (...) VALUES (...) RETURNING *;` | Returns inserted rows. |
| `UPDATE table_name SET ... RETURNING *;` | Returns updated rows. |
| `DELETE FROM table_name RETURNING *;` | Returns deleted rows. |

#### **Example**
```sql
UPDATE employees SET salary = 70000 WHERE id = 2 RETURNING *;
```

---

## **8. Transaction Control in DML**  
DML statements are **affected by transactions**, allowing rollback and commit operations.

| **Command** | **Description** |
|------------|---------------|
| `BEGIN;` | Starts a transaction. |
| `COMMIT;` | Saves changes permanently. |
| `ROLLBACK;` | Undoes all changes in the transaction. |
| `SAVEPOINT sp_name;` | Creates a savepoint in a transaction. |
| `ROLLBACK TO sp_name;` | Rolls back to a specific savepoint. |

#### **Example**
```sql
BEGIN;
UPDATE employees SET salary = 75000 WHERE id = 2;
ROLLBACK; -- Undo the update
```

---

## **Key Takeaways**  
- **DML allows manipulation of data** in tables.  
- **INSERT adds data**, **UPDATE modifies existing records**, and **DELETE removes data**.  
- **SELECT retrieves data** with filtering, sorting, and limits.  
- **RETURNING retrieves affected rows** after DML operations.  
- **Transactions ensure data consistency** by using `BEGIN`, `COMMIT`, and `ROLLBACK`.  
