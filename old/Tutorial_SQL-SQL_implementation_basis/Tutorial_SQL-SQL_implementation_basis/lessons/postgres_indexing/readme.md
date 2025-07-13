## **PostgreSQL Indexing: Comprehensive Cheatsheet**  

---

### **1. Overview of Indexing**  
| Feature | Description |
|---------|-------------|
| Purpose | Speeds up data retrieval by reducing the number of rows scanned. |
| Default Index | `PRIMARY KEY` and `UNIQUE` constraints automatically create `B-TREE` indexes. |
| Custom Indexing | Can be created on columns or expressions. |
| Types | `B-TREE`, `HASH`, `GIN`, `GiST`, `SP-GiST`, `BRIN`. |

---

### **2. Creating Indexes**  
**Basic Index:**  
```sql
CREATE INDEX idx_column_name ON table_name (column_name);
```
**Unique Index:**  
```sql
CREATE UNIQUE INDEX idx_unique_email ON users (email);
```
**Multicolumn Index:**  
```sql
CREATE INDEX idx_multi_col ON employees (last_name, first_name);
```
**Expression Index:**  
```sql
CREATE INDEX idx_lower_name ON users (LOWER(name));
```

---

### **3. Types of Indexes**  
| Index Type | Use Case | Example |
|------------|---------|---------|
| `B-TREE` | Default index; best for range, equality, sorting, and `ORDER BY`. | `CREATE INDEX idx_bt ON users (email);` |
| `HASH` | Fast for equality lookups (`=`) but not for range queries. | `CREATE INDEX idx_hash ON users USING HASH (email);` |
| `GIN` | Best for `ARRAY`, `JSONB`, and full-text search. | `CREATE INDEX idx_gin ON documents USING GIN (content);` |
| `GiST` | Used for geometric and full-text search indexing. | `CREATE INDEX idx_gist ON locations USING GiST (coordinates);` |
| `SP-GiST` | Good for non-balanced tree structures, like hierarchical data. | `CREATE INDEX idx_spgist ON roads USING SPGIST (route);` |
| `BRIN` | Efficient for large, naturally ordered datasets. | `CREATE INDEX idx_brin ON logs USING BRIN (timestamp);` |

---

### **4. Indexing for Performance Optimization**  
| Optimization | Index Type | Example |
|-------------|-----------|---------|
| Faster `SELECT` queries | `B-TREE` | `CREATE INDEX idx_lastname ON employees (last_name);` |
| JSONB queries | `GIN` | `CREATE INDEX idx_jsonb ON users USING GIN (preferences);` |
| Text search | `GIN` with `to_tsvector` | `CREATE INDEX idx_text ON articles USING GIN (to_tsvector('english', content));` |
| Faster `LIKE` queries | `B-TREE` on `LOWER(column)` | `CREATE INDEX idx_lower_name ON users (LOWER(name));` |
| Spatial queries | `GiST` | `CREATE INDEX idx_spatial ON locations USING GiST (geom);` |

---

### **5. Partial Indexes**  
| Feature | Description |
|---------|-------------|
| Index only specific rows | Reduces index size, improving performance |
| Useful for filtering active records | Example: indexing only active users |

**Example:**  
```sql
CREATE INDEX idx_active_users ON users (email) WHERE status = 'active';
```

---

### **6. Covering Index (Index-Only Scan)**  
| Feature | Description |
|---------|-------------|
| Stores extra column data in the index | Avoids accessing the main table for `SELECT` queries |

**Example:**  
```sql
CREATE INDEX idx_covering ON employees (last_name, first_name) INCLUDE (salary);
```

---

### **7. Dropping Indexes**  
**Drop a single index:**  
```sql
DROP INDEX idx_column_name;
```
**Drop an index if it exists:**  
```sql
DROP INDEX IF EXISTS idx_column_name;
```

---

### **8. Rebuilding Indexes**  
**Rebuild an index manually:**  
```sql
REINDEX INDEX idx_column_name;
```
**Rebuild all indexes on a table:**  
```sql
REINDEX TABLE employees;
```

---

### **9. Checking Index Usage**  
**List all indexes in a database:**  
```sql
SELECT * FROM pg_indexes WHERE schemaname = 'public';
```
**Analyze query performance with indexing:**  
```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'user@example.com';
```
