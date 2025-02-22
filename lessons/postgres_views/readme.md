## **PostgreSQL Views: Comprehensive Cheatsheet**  

---

### **1. Overview of Views**  
| Feature | Description |
|---------|-------------|
| **Definition** | A stored SQL query that presents data as a virtual table. |
| **Purpose** | Simplifies queries, improves security, and enhances performance. |
| **Types** | Regular Views, Materialized Views. |
| **Usage** | Can be queried like a regular table (`SELECT * FROM view_name`). |

---

### **2. Creating a View**  
| Feature | Description |
|---------|-------------|
| Stores query results as a virtual table | No data is physically stored. |

**Syntax:**  
```sql
CREATE VIEW view_name AS 
SELECT column1, column2 
FROM table_name 
WHERE condition;
```

**Example:**  
```sql
CREATE VIEW active_users AS 
SELECT id, name, email 
FROM users 
WHERE status = 'active';
```

---

### **3. Querying a View**  
**Syntax:**  
```sql
SELECT * FROM view_name;
```
**Example:**  
```sql
SELECT * FROM active_users;
```

---

### **4. Updating a View**  
| Feature | Description |
|---------|-------------|
| Views do not store data | They reflect real-time changes in the base tables. |

**To update the view definition:**  
```sql
CREATE OR REPLACE VIEW view_name AS 
SELECT column1, column2 FROM table_name WHERE condition;
```

**Example:**  
```sql
CREATE OR REPLACE VIEW active_users AS 
SELECT id, name, email, created_at 
FROM users 
WHERE status = 'active';
```

---

### **5. Dropping a View**  
| Feature | Description |
|---------|-------------|
| Removes the view but not the underlying data | Use `IF EXISTS` to prevent errors. |

**Syntax:**  
```sql
DROP VIEW IF EXISTS view_name;
```
**Example:**  
```sql
DROP VIEW IF EXISTS active_users;
```

---

### **6. Updatable Views**  
| Feature | Description |
|---------|-------------|
| Allows `INSERT`, `UPDATE`, and `DELETE` if conditions are met | Must be based on a single table with no aggregations or joins. |

**Example:**  
```sql
CREATE VIEW updatable_users AS 
SELECT id, name, email FROM users 
WHERE status = 'active';
```
```sql
UPDATE updatable_users SET email = 'new@example.com' WHERE id = 1;
```

---

### **7. Materialized Views**  
| Feature | Description |
|---------|-------------|
| Stores query results physically | Needs manual refresh (`REFRESH MATERIALIZED VIEW`). |
| Improves performance | Faster for large datasets. |

**Creating a Materialized View:**  
```sql
CREATE MATERIALIZED VIEW mat_view_name AS 
SELECT column1, column2 
FROM table_name 
WHERE condition;
```
**Example:**  
```sql
CREATE MATERIALIZED VIEW active_users_mat AS 
SELECT id, name, email FROM users WHERE status = 'active';
```

**Refreshing a Materialized View:**  
```sql
REFRESH MATERIALIZED VIEW active_users_mat;
```

**Dropping a Materialized View:**  
```sql
DROP MATERIALIZED VIEW active_users_mat;
```

---

### **8. Performance Optimization**  
| Optimization | Description |
|-------------|-------------|
| **Indexes** | Index columns in the base table used in the view. |
| **Materialized Views** | Use for static data that doesn’t change frequently. |
| **`WITH CHECK OPTION`** | Prevents inserting/updating rows that don’t satisfy view conditions. |

**Example:**  
```sql
CREATE VIEW active_users_secure AS 
SELECT id, name, email FROM users WHERE status = 'active'
WITH CHECK OPTION;
```
