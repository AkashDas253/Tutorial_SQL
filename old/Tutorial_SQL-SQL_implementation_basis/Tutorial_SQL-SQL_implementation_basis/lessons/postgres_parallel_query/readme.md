## **PostgreSQL Parallel Query Execution: Comprehensive Cheatsheet**  

---

## **1. Key Concepts**  
| Feature | Description |
|---------|-------------|
| **Parallel Query Execution** | Splits queries into multiple processes to utilize multiple CPU cores. |
| **Automatic Usage** | PostgreSQL automatically determines when to use parallel execution based on query complexity and cost. |
| **Worker Processes** | Uses background worker processes (`parallel workers`) to execute parts of the query. |
| **Cost-Based Optimization** | Queries with high execution cost (`parallel_tuple_cost`, `parallel_setup_cost`) are more likely to use parallelism. |

---

## **2. Enabling Parallel Queries**  
| Setting | Purpose | Default |
|---------|---------|---------|
| `max_parallel_workers_per_gather` | Maximum workers per parallel query. | 2 |
| `parallel_tuple_cost` | Cost of processing a tuple in parallel. | 0.1 |
| `parallel_setup_cost` | Cost of setting up parallel workers. | 1000 |
| `force_parallel_mode` | Enforce parallel execution for testing. | `off` |

### **Adjusting Parallel Worker Configuration**  
```sql
ALTER SYSTEM SET max_parallel_workers_per_gather = 4;
ALTER SYSTEM SET parallel_tuple_cost = 0.01;
ALTER SYSTEM SET parallel_setup_cost = 100;
```
```sh
SELECT pg_reload_conf();
```

---

## **3. Query Types That Use Parallel Execution**  
| Query Type | Supports Parallelism? |
|-----------|---------------------|
| **`SELECT` (Aggregations, Joins, Scans)** | ✅ Yes |
| **`CREATE INDEX` (B-tree, GIN, GiST, BRIN)** | ✅ Yes |
| **`UPDATE` / `DELETE`** | ❌ No (Not parallelized) |
| **CTEs (`WITH` Queries)** | ⚠ Partial (Only if inline-able) |

---

## **4. Checking Parallel Execution in Queries**  

### **Explain Plan for Parallel Queries**
```sql
EXPLAIN ANALYZE SELECT COUNT(*) FROM large_table;
```
**Output Example:**
```
Gather  
  Workers Planned: 4  
  -> Parallel Seq Scan on large_table  
```

### **Disabling Parallel Execution for a Query**
```sql
SET parallel_tuple_cost = 1000000;
SET parallel_setup_cost = 1000000;
```
OR
```sql
SELECT /*+ DisableParallel */ COUNT(*) FROM large_table;
```

---

## **5. Parallel Indexing**
| Index Type | Supports Parallelism? |
|-----------|---------------------|
| **B-tree** | ✅ Yes |
| **GIN / GiST / BRIN** | ✅ Yes |
| **Hash Index** | ❌ No |

### **Creating an Index with Parallel Execution**
```sql
CREATE INDEX CONCURRENTLY idx_large_table ON large_table (column_name);
```

---

## **6. Optimizing for Parallel Queries**
| Optimization | Description |
|-------------|-------------|
| **Increase `max_parallel_workers_per_gather`** | Allows more worker processes to handle queries. |
| **Use Parallel-Safe Functions** | Ensure functions used in queries do not block parallel execution. |
| **Avoid Parallel Restrictive Operations** | `PL/pgSQL`, temporary tables, and volatile functions disable parallelism. |
