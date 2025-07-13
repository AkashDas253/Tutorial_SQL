## **PostgreSQL JSON & JSONB Data Type, Functions, and Operations**  

---

### **1. JSON vs. JSONB**  
| Feature | `JSON` | `JSONB` |
|---------|-------|--------|
| Storage | Text-based | Binary format |
| Read Performance | Slower | Faster (indexed) |
| Write Performance | Faster | Slower (due to parsing) |
| Indexing | No indexing | Supports indexing |
| Duplicate Keys | Preserved | Removed (last key wins) |
| Processing | Stored as-is | Stored in a structured way |

---

### **2. JSON & JSONB Data Types**  
| Data Type | Description |
|-----------|-------------|
| `JSON` | Stores unprocessed JSON text |
| `JSONB` | Stores JSON in a decomposed binary format |

---

### **3. JSON & JSONB Operators**  
| Operator | Description | Example | Output |
|----------|-------------|---------|--------|
| `->` | Get JSON object field (as JSON) | `json_data->'name'` | `"John"` |
| `->>` | Get JSON object field (as text) | `json_data->>'name'` | `John` |
| `#>` | Get nested JSON object (as JSON) | `json_data#>'{address, city}'` | `"New York"` |
| `#>>` | Get nested JSON object (as text) | `json_data#>>'{address, city}'` | `New York` |
| `@>` | JSON contains another JSON | `json_data @> '{"name": "John"}'` | `TRUE` |
| `<@` | JSON is contained in another JSON | `json_data <@ '{"name": "John", "age": 30}'` | `TRUE` |
| `?` | Check if key exists | `json_data ? 'name'` | `TRUE` |
| `?|` | Check if any key exists | `json_data ?| array['name', 'age']` | `TRUE` |
| `?&` | Check if all keys exist | `json_data ?& array['name', 'age']` | `TRUE` |
| `-` | Remove a key | `json_data - 'name'` | Removes `"name"` |
| `#-` | Remove a nested key | `json_data #- '{address, city}'` | Removes `"city"` |

---

### **4. JSON Functions**  
| Function | Description | Example | Output |
|----------|-------------|---------|--------|
| `jsonb_pretty(jsonb)` | Formats JSONB for readability | `SELECT jsonb_pretty('{"name": "John"}');` | `{\n  "name": "John"\n}` |
| `jsonb_each(jsonb)` | Expands JSONB into key-value pairs | `SELECT jsonb_each('{"name": "John", "age": 30}');` | `name | "John"`, `age | 30` |
| `jsonb_object_keys(jsonb)` | Extracts top-level keys | `SELECT jsonb_object_keys('{"name": "John", "age": 30}');` | `name`, `age` |
| `jsonb_array_elements(jsonb)` | Expands JSONB array into rows | `SELECT jsonb_array_elements('[1,2,3]');` | `1`, `2`, `3` |

---

### **5. Querying JSON Data**  
#### **Extracting Fields**
```sql
SELECT data->>'name' AS name FROM users;
```
#### **Filtering Data**
```sql
SELECT * FROM users WHERE data->>'age' = '30';
```
#### **Checking Key Existence**
```sql
SELECT * FROM users WHERE data ? 'email';
```
#### **Indexing JSONB**
```sql
CREATE INDEX users_data_idx ON users USING gin (data);
```
