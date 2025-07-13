## **PostgreSQL JSON Support: Comprehensive Cheatsheet**  

---

## **1. JSON Data Types in PostgreSQL**  
| Data Type | Description |
|-----------|-------------|
| **JSON**  | Stores data as a plain text JSON string (no indexing, slower). |
| **JSONB** | Stores data in a binary format (supports indexing, faster queries). |

### **Choosing Between JSON and JSONB**  
| Feature | JSON | JSONB |
|---------|------|-------|
| Storage Format | Text | Binary |
| Indexing | ❌ No | ✅ Yes |
| Read Performance | Slower | Faster |
| Write Performance | Faster | Slower (due to conversion) |
| Supports Operators & Functions | ✅ Yes | ✅ Yes |

---

## **2. Creating JSON/JSONB Columns**  
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    details JSONB
);
```

---

## **3. Inserting JSON Data**  
```sql
INSERT INTO users (details) 
VALUES ('{"name": "Alice", "age": 30, "city": "New York"}');
```

---

## **4. Querying JSON Data**  
| Method | Query |
|--------|-------|
| **Retrieve Entire JSON** | `SELECT details FROM users;` |
| **Access JSON Field (`->`)** | `SELECT details->'name' FROM users;` |
| **Access JSON Field as Text (`->>`)** | `SELECT details->>'name' FROM users;` |
| **Filter by JSON Value** | `SELECT * FROM users WHERE details->>'city' = 'New York';` |

---

## **5. JSONB Indexing for Faster Queries**  
```sql
CREATE INDEX idx_users_details ON users USING GIN (details);
```

---

## **6. Modifying JSON Data**  
| Operation | Query |
|-----------|-------|
| **Update a JSON Field** | `UPDATE users SET details = jsonb_set(details, '{age}', '31') WHERE id = 1;` |
| **Remove a JSON Key** | `UPDATE users SET details = details - 'city' WHERE id = 1;` |

---

## **7. JSON Aggregation & Functions**  
| Function | Description |
|----------|-------------|
| `jsonb_each()` | Expands JSONB into key-value pairs. |
| `jsonb_object_keys()` | Returns all keys in a JSONB object. |
| `jsonb_array_elements()` | Expands JSON arrays into individual rows. |

### **Example: Extracting JSON Keys**
```sql
SELECT jsonb_object_keys(details) FROM users;
```
