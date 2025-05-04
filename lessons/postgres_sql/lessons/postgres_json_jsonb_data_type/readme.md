### PostgreSQL JSON & JSONB Data Types  

#### Overview  
- **`json`**: Stores raw JSON data as a text string.  
- **`jsonb`**: Stores JSON in a binary format with indexing and efficient querying.  

#### Key Differences  
| Feature | `json` | `jsonb` |
|---------|-------|--------|
| Storage | Text format | Binary format |
| Indexing | Not supported | Supports indexing |
| Query Performance | Slower | Faster (optimized for queries) |
| Order Preservation | Yes | No (key order is not maintained) |
| Supports GIN Indexing | No | Yes (efficient searching) |

#### Example Table  
```sql
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    details JSONB  -- Use JSONB for better performance
);
```

#### Inserting JSON Data  
```sql
INSERT INTO products (details) 
VALUES ('{"name": "Laptop", "price": 1000, "specs": {"ram": "16GB", "storage": "512GB"}}');
```

#### Querying JSON Data  
| Query | Example |
|-------|---------|
| Retrieve full JSON | `SELECT details FROM products;` |
| Retrieve a specific key | `SELECT details->>'name' FROM products;` |
| Retrieve nested key | `SELECT details->'specs'->>'ram' FROM products;` |
| Filter JSON field | `SELECT * FROM products WHERE details->>'price' = '1000';` |

#### Indexing JSONB  
For efficient searching, use a **GIN index**:  
```sql
CREATE INDEX idx_products_details ON products USING GIN (details);
```

#### When to Use  
| Scenario | Recommended Type |
|----------|----------------|
| Storing JSON as a simple string | `json` |
| Fast querying and indexing | `jsonb` |
| Storing large and complex JSON data | `jsonb` |

---