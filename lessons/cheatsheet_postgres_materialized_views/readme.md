## **PostgreSQL Materialized Views: Comprehensive Cheatsheet**  

---

### **1. Overview of Materialized Views**  
| Feature | Description |
|---------|-------------|
| **Definition** | A stored query result that persists physically, unlike regular views. |
| **Purpose** | Improves query performance by caching results of complex queries. |
| **Data Storage** | Stores results physically in the database. |
| **Refresh Mechanism** | Requires manual or scheduled refresh to update data. |

---

### **2. Creating a Materialized View**  
| Feature | Description |
|---------|-------------|
| Stores query results | Improves performance for complex joins, aggregations, and computations. |

**Syntax:**  
```sql
CREATE MATERIALIZED VIEW view_name AS 
SELECT column1, column2 FROM table_name 
WHERE condition;
```

**Example:**  
```sql
CREATE MATERIALIZED VIEW active_users_mat AS 
SELECT id, name, email FROM users 
WHERE status = 'active';
```

---

### **3. Querying a Materialized View**  
**Syntax:**  
```sql
SELECT * FROM view_name;
```

**Example:**  
```sql
SELECT * FROM active_users_mat;
```

---

### **4. Refreshing a Materialized View**  
| Feature | Description |
|---------|-------------|
| Unlike regular views, materialized views do not update automatically | Must be refreshed manually or scheduled. |

**Manual Refresh:**  
```sql
REFRESH MATERIALIZED VIEW view_name;
```

**Example:**  
```sql
REFRESH MATERIALIZED VIEW active_users_mat;
```

**Refreshing with Concurrent Access:**  
```sql
REFRESH MATERIALIZED VIEW CONCURRENTLY view_name;
```
**Requirement:** The view must have a **unique index** to support concurrent refresh.

**Example:**  
```sql
CREATE UNIQUE INDEX idx_active_users ON active_users_mat (id);
REFRESH MATERIALIZED VIEW CONCURRENTLY active_users_mat;
```

---

### **5. Dropping a Materialized View**  
| Feature | Description |
|---------|-------------|
| Deletes the stored data and view definition | Use `IF EXISTS` to prevent errors. |

**Syntax:**  
```sql
DROP MATERIALIZED VIEW IF EXISTS view_name;
```

**Example:**  
```sql
DROP MATERIALIZED VIEW IF EXISTS active_users_mat;
```

---

### **6. Performance Considerations**  
| Optimization | Description |
|-------------|-------------|
| **Indexes** | Create indexes on materialized view columns to improve query performance. |
| **Use `WITH DATA`** | Stores the query result at creation (default behavior). |
| **Use `WITH NO DATA`** | Creates the view without populating data (must be refreshed manually). |

**Example (Creating without data):**  
```sql
CREATE MATERIALIZED VIEW active_users_mat 
AS SELECT id, name, email FROM users 
WHERE status = 'active' WITH NO DATA;
```
```sql
REFRESH MATERIALIZED VIEW active_users_mat;
```
