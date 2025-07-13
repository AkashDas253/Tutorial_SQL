### PostgreSQL Boolean Data Type  

#### Overview  
- **Data Type:** `boolean`  
- **Size:** 1 byte  
- **Possible Values:**  
  | Value | Equivalent Representation |  
  |--------|-------------------------|  
  | `TRUE`  | `true`, `t`, `yes`, `y`, `on`, `1` |  
  | `FALSE` | `false`, `f`, `no`, `n`, `off`, `0` |  
  | `NULL`  | Represents an unknown state |  

#### Key Features  
- Stored as a **single byte**, making it space-efficient.  
- `NULL` is not the same as `FALSE`; it represents an unknown value.  

#### Usage Scenarios  
| Scenario | Example |  
|----------|---------|  
| Status flags (active/inactive) | `is_active BOOLEAN` |  
| Feature toggles (enabled/disabled) | `is_enabled BOOLEAN` |  
| Logical conditions in queries | `WHERE is_verified = TRUE` |  

#### Example Usage  
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    is_active BOOLEAN DEFAULT TRUE
);

INSERT INTO users (name, is_active) VALUES ('Alice', TRUE);
SELECT * FROM users WHERE is_active = FALSE;
```

---