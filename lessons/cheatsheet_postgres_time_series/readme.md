## **PostgreSQL Time-Series Data - Comprehensive Cheatsheet**  

---

## **1. Key Concepts**  

| Feature | Description |
|---------|-------------|
| **Time-Series Data** | Data indexed by time, often used for monitoring, logs, IoT, finance, etc. |
| **Indexing** | `B-Tree` (default), `BRIN` (for large datasets). |
| **Partitioning** | Improves performance by splitting data into smaller tables. |
| **Continuous Aggregates** | Stores precomputed results for faster queries. |
| **TimescaleDB** | PostgreSQL extension optimized for time-series data. |

---

## **2. Table Design for Time-Series Data**  

### **Basic Table Structure**  
```sql
CREATE TABLE sensor_data (
    sensor_id INT,
    timestamp TIMESTAMPTZ DEFAULT NOW(),
    temperature FLOAT,
    humidity FLOAT,
    PRIMARY KEY (sensor_id, timestamp)
);
```

### **BRIN Index for Large Datasets**  
```sql
CREATE INDEX sensor_data_brin ON sensor_data USING BRIN (timestamp);
```
- Efficient for **append-only** time-series data.

---

## **3. Inserting Time-Series Data**  

```sql
INSERT INTO sensor_data (sensor_id, timestamp, temperature, humidity)
VALUES (1, NOW(), 22.5, 60.2);
```

- Uses `NOW()` for automatic timestamp assignment.

---

## **4. Querying Time-Series Data**  

### **Retrieve Data for a Specific Time Range**  
```sql
SELECT * FROM sensor_data  
WHERE timestamp BETWEEN '2024-02-01' AND '2024-02-10';
```

### **Get the Latest Data for Each Sensor**  
```sql
SELECT DISTINCT ON (sensor_id) *  
FROM sensor_data  
ORDER BY sensor_id, timestamp DESC;
```

### **Average Temperature per Day**  
```sql
SELECT DATE(timestamp) AS day, AVG(temperature)  
FROM sensor_data  
GROUP BY day  
ORDER BY day;
```

---

## **5. Partitioning for Performance**  

### **Create a Partitioned Table**  
```sql
CREATE TABLE sensor_data (
    sensor_id INT,
    timestamp TIMESTAMPTZ NOT NULL,
    temperature FLOAT,
    humidity FLOAT,
    PRIMARY KEY (sensor_id, timestamp)
) PARTITION BY RANGE (timestamp);
```

### **Create Partitions by Month**  
```sql
CREATE TABLE sensor_data_2024_01  
PARTITION OF sensor_data  
FOR VALUES FROM ('2024-01-01') TO ('2024-02-01');
```

### **Automatic Partitioning with Triggers**  
```sql
CREATE OR REPLACE FUNCTION insert_sensor_data()  
RETURNS TRIGGER AS $$  
BEGIN  
    EXECUTE format('INSERT INTO sensor_data_%s VALUES ($1.*)',  
                   to_char(NEW.timestamp, 'YYYY_MM'))  
    USING NEW;  
    RETURN NULL;  
END;  
$$ LANGUAGE plpgsql;

CREATE TRIGGER sensor_data_insert  
BEFORE INSERT ON sensor_data  
FOR EACH ROW EXECUTE FUNCTION insert_sensor_data();
```

---

## **6. Aggregating Data Efficiently**  

### **Rolling Average (7 Days)**  
```sql
SELECT timestamp,  
       AVG(temperature) OVER (ORDER BY timestamp ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)  
FROM sensor_data;
```

### **Downsampling Data (Hourly Averages)**  
```sql
SELECT date_trunc('hour', timestamp) AS hour,  
       AVG(temperature) AS avg_temp  
FROM sensor_data  
GROUP BY hour  
ORDER BY hour;
```

---

## **7. Advanced Optimization Techniques**  

| Optimization | Description |
|-------------|-------------|
| **Indexes** | Use `BRIN` for large datasets, `B-Tree` for smaller ones. |
| **Partitioning** | Store data in smaller partitions for faster queries. |
| **Continuous Aggregates** | Precompute data using materialized views. |
| **Connection Pooling** | Use `PgBouncer` to manage concurrent queries. |
| **TimescaleDB** | Use for advanced time-series capabilities. |
