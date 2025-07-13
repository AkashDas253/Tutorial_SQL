## **PostgreSQL Partitioning: Comprehensive Cheatsheet**  

---

## **1. Types of Partitioning**  
| Partitioning Type | Description |
|------------------|-------------|
| **Range Partitioning** | Divides data based on value ranges (e.g., date ranges). |
| **List Partitioning** | Divides data based on discrete values (e.g., categories, regions). |
| **Hash Partitioning** | Uses a hash function to evenly distribute data across partitions. |
| **Composite Partitioning** | Combines multiple partitioning strategies (e.g., range + hash). |

---

## **2. Creating Partitioned Tables**  

### **Range Partitioning Example (By Date)**  
```sql
CREATE TABLE sales (
    id SERIAL,
    sale_date DATE NOT NULL,
    amount NUMERIC
) PARTITION BY RANGE (sale_date);

CREATE TABLE sales_2024 PARTITION OF sales 
    FOR VALUES FROM ('2024-01-01') TO ('2024-12-31');
```

### **List Partitioning Example (By Region)**  
```sql
CREATE TABLE customers (
    id SERIAL,
    region TEXT NOT NULL
) PARTITION BY LIST (region);

CREATE TABLE customers_us PARTITION OF customers 
    FOR VALUES IN ('US');

CREATE TABLE customers_eu PARTITION OF customers 
    FOR VALUES IN ('EU');
```

### **Hash Partitioning Example (Even Distribution)**  
```sql
CREATE TABLE transactions (
    id SERIAL,
    user_id INT NOT NULL
) PARTITION BY HASH (user_id);

CREATE TABLE transactions_p0 PARTITION OF transactions 
    FOR VALUES WITH (MODULUS 4, REMAINDER 0);

CREATE TABLE transactions_p1 PARTITION OF transactions 
    FOR VALUES WITH (MODULUS 4, REMAINDER 1);
```

---

## **3. Inserting & Querying Partitioned Tables**  
| Operation | Query |
|-----------|-------|
| **Insert Data** | `INSERT INTO sales VALUES (1, '2024-06-15', 100.00);` |
| **Query with Partition Pruning** | `SELECT * FROM sales WHERE sale_date BETWEEN '2024-01-01' AND '2024-06-30';` |

---

## **4. Managing Partitions**  
| Operation | Query |
|-----------|-------|
| **Add a New Partition** | `CREATE TABLE sales_2025 PARTITION OF sales FOR VALUES FROM ('2025-01-01') TO ('2025-12-31');` |
| **Detach a Partition** | `ALTER TABLE sales DETACH PARTITION sales_2024;` |
| **Drop a Partition** | `DROP TABLE sales_2024;` |

---

## **5. Performance Considerations**  
| Best Practice | Description |
|--------------|-------------|
| **Use Indexes** | Indexes should be created separately for each partition. |
| **Enable Partition Pruning** | Query optimizer automatically ignores irrelevant partitions. |
| **Avoid Too Many Partitions** | Excessive partitions may impact performance. |
