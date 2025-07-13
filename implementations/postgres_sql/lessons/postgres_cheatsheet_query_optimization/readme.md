## **PostgreSQL Query Optimization: Comprehensive Cheatsheet**  

---

## **1. General Optimization Techniques**  
| Technique | Description |
|-----------|-------------|
| **Use Indexing** | Improve query performance by creating appropriate indexes. |
| **Avoid `SELECT *`** | Fetch only required columns to reduce I/O load. |
| **Use Proper Data Types** | Choose efficient data types to save space and speed up operations. |
| **Use `EXPLAIN ANALYZE`** | Analyze query execution plans for performance bottlenecks. |
| **Normalize Tables** | Reduce redundancy for efficient queries. |
| **Denormalize for Reads** | Use materialized views or redundant columns for read-heavy workloads. |

---

## **2. Index Optimization**  
| Index Type | Use Case |
|------------|---------|
| **B-Tree Index** | Default index, good for equality and range queries. |
| **Hash Index** | Optimized for equality comparisons (`=`). |
| **GIN Index** | Used for full-text search and JSONB data. |
| **GiST Index** | Supports geometric and full-text search. |
| **BRIN Index** | Efficient for very large tables with ordered data. |
| **Partial Index** | Index only part of the table to save space. |
| **Covering Index** | Includes additional columns to avoid lookups. |

### **Example: Creating Indexes**
```sql
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_orders_status ON orders(status) WHERE status = 'shipped';
```

---

## **3. Query Execution Analysis**  
| Command | Description |
|---------|-------------|
| `EXPLAIN` | Shows the query execution plan without running it. |
| `EXPLAIN ANALYZE` | Executes the query and provides execution statistics. |
| `EXPLAIN (BUFFERS, COSTS, ANALYZE, TIMING)` | Provides detailed insights into buffer usage and execution costs. |

### **Example: Analyzing a Query**
```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'test@example.com';
```

---

## **4. Optimizing Joins**  
| Join Type | Optimization Strategy |
|-----------|----------------------|
| **Nested Loop Join** | Used when one table is small and indexed. |
| **Hash Join** | Best for large, non-indexed datasets. |
| **Merge Join** | Used when both tables are sorted. |
| **Avoid Cross Joins** | Filter data before joining to avoid Cartesian products. |

### **Example: Optimized Join**
```sql
SELECT u.name, o.total 
FROM users u 
JOIN orders o ON u.id = o.user_id 
WHERE o.status = 'completed';
```

---

## **5. Optimizing Aggregations & Grouping**  
| Technique | Description |
|-----------|-------------|
| **Use Indexes on Grouping Columns** | Helps speed up `GROUP BY` operations. |
| **Use `HAVING` Carefully** | Filter data using `WHERE` before aggregating. |
| **Use `FILTER` Instead of `CASE`** | Improves readability and performance. |

### **Example: Using `FILTER` for Conditional Aggregation**
```sql
SELECT 
    user_id, 
    COUNT(*) FILTER (WHERE status = 'completed') AS completed_orders 
FROM orders 
GROUP BY user_id;
```

---

## **6. Optimizing Subqueries**  
| Technique | Description |
|-----------|-------------|
| **Use Joins Instead of Correlated Subqueries** | Improves performance by avoiding repeated execution. |
| **Use CTEs (`WITH` Clause)** | Helps break down complex queries and improve readability. |
| **Use `EXISTS` Instead of `IN`** | More efficient for checking existence in large datasets. |

### **Example: Replacing `IN` with `EXISTS`**
```sql
SELECT * FROM users u
WHERE EXISTS (
    SELECT 1 FROM orders o WHERE o.user_id = u.id AND o.status = 'completed'
);
```

---

## **7. Caching & Materialized Views**  
| Technique | Description |
|-----------|-------------|
| **Use Materialized Views** | Precompute expensive queries for faster reads. |
| **Use Connection Pooling** | Reduce overhead for frequent queries. |
| **Use `pg_stat_statements`** | Analyze query performance trends. |

### **Example: Creating & Refreshing a Materialized View**
```sql
CREATE MATERIALIZED VIEW recent_orders AS
SELECT * FROM orders WHERE created_at > NOW() - INTERVAL '7 days';

REFRESH MATERIALIZED VIEW recent_orders;
```

---

## **8. Optimizing Large Tables**  
| Technique | Description |
|-----------|-------------|
| **Use Partitioning** | Divide large tables for better performance. |
| **Use `VACUUM` & `ANALYZE`** | Prevent table bloat and update statistics. |
| **Use Parallel Queries** | Enable multi-threaded execution for large datasets. |

### **Example: Table Partitioning**
```sql
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    order_date DATE NOT NULL
) PARTITION BY RANGE (order_date);

CREATE TABLE orders_2024 PARTITION OF orders 
FOR VALUES FROM ('2024-01-01') TO ('2024-12-31');
```

---

## **9. Performance Monitoring & Tuning**  
| Command | Description |
|---------|-------------|
| `pg_stat_activity` | View currently running queries. |
| `pg_stat_statements` | Monitor query execution statistics. |
| `pg_indexes_size('table_name')` | Check index sizes. |
| `pg_table_size('table_name')` | Check table sizes. |

### **Example: Checking Running Queries**
```sql
SELECT * FROM pg_stat_activity;
```

---
