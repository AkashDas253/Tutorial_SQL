## **PostgreSQL Performance Monitoring - Comprehensive Cheatsheet**  

---

## **1. Key Concepts**  
| Feature | Description |
|---------|-------------|
| **Performance Monitoring** | Tracks database metrics, query execution, and system load. |
| **pg_stat_activity** | Monitors active queries and connections. |
| **pg_stat_statements** | Tracks query execution statistics. |
| **EXPLAIN ANALYZE** | Provides execution plans for queries. |
| **Logging** | Stores slow queries and errors. |

---

## **2. System Performance Monitoring**  

| Metric | Query |
|--------|-------|
| **Database Size** | `SELECT pg_size_pretty(pg_database_size('dbname'));` |
| **Table Size** | `SELECT pg_size_pretty(pg_total_relation_size('table_name'));` |
| **Active Connections** | `SELECT * FROM pg_stat_activity;` |
| **Blocked Queries** | `SELECT * FROM pg_locks WHERE granted = false;` |
| **Vacuum Status** | `SELECT * FROM pg_stat_all_tables WHERE last_autovacuum IS NOT NULL;` |

---

## **3. Query Performance Monitoring**  

### **Track Long-Running Queries**  
```sql
SELECT pid, age(clock_timestamp(), query_start) AS duration, query  
FROM pg_stat_activity  
WHERE state = 'active'  
ORDER BY duration DESC;
```

### **Identify Slow Queries Using pg_stat_statements**  
```sql
SELECT query, calls, total_time, mean_time  
FROM pg_stat_statements  
ORDER BY total_time DESC  
LIMIT 5;
```

### **Analyze Query Execution Plan**  
```sql
EXPLAIN ANALYZE SELECT * FROM table_name WHERE column = 'value';
```
- Identifies query performance bottlenecks.

---

## **4. Index Usage Monitoring**  

| Metric | Query |
|--------|-------|
| **Unused Indexes** | `SELECT * FROM pg_stat_user_indexes WHERE idx_scan = 0;` |
| **Index Hit Ratio** | ```sql  
SELECT relname,  
       (100 * idx_blks_hit / (idx_blks_hit + idx_blks_read)) AS hit_ratio  
FROM pg_statio_user_indexes;  
``` |
| **Missing Indexes** | `EXPLAIN ANALYZE` on slow queries to check for sequential scans. |

---

## **5. Connection & Lock Monitoring**  

### **Monitor Connection Usage**  
```sql
SELECT count(*), state FROM pg_stat_activity GROUP BY state;
```
- Checks active vs idle connections.

### **Monitor Lock Conflicts**  
```sql
SELECT pid, relation::regclass, mode, granted  
FROM pg_locks  
WHERE NOT granted;
```
- Identifies blocked queries.

---

## **6. Autovacuum & Bloat Monitoring**  

### **Check Autovacuum Activity**  
```sql
SELECT relname, last_autovacuum, last_autoanalyze  
FROM pg_stat_all_tables  
WHERE last_autovacuum IS NOT NULL;
```

### **Check Table Bloat**  
```sql
SELECT relname, pg_size_pretty(pg_table_size(relid)) AS table_size,  
       pg_size_pretty(pg_total_relation_size(relid) - pg_table_size(relid)) AS bloat  
FROM pg_stat_user_tables;
```

---

## **7. Logs & Error Monitoring**  

| Setting | Configuration (postgresql.conf) |
|---------|-------------------------------|
| **Enable Logging** | `logging_collector = on` |
| **Log Slow Queries** | `log_min_duration_statement = 1000` (Logs queries > 1 sec) |
| **Log Deadlocks** | `log_lock_waits = on` |

### **Check Logs for Errors**  
```sh
tail -f /var/log/postgresql/postgresql.log
```

---

## **8. Performance Optimization Tips**  
| Optimization | Description |
|-------------|-------------|
| **Use Indexes** | Ensure proper indexing to avoid sequential scans. |
| **Analyze & Vacuum** | Run `ANALYZE` and `VACUUM` to update statistics. |
| **Optimize Queries** | Use `EXPLAIN ANALYZE` to refine slow queries. |
| **Connection Pooling** | Use `PgBouncer` to manage connections efficiently. |
| **Tune Work Memory** | Increase `work_mem` for complex queries. |
