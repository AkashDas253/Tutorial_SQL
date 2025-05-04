### PostgreSQL Array Data Type  

#### Overview  
- PostgreSQL supports **arrays** of any data type, including integers, text, booleans, and even user-defined types.  
- Arrays can store **multiple values in a single column**, making them useful for storing lists or sets of related data.  

#### Syntax  
```sql
data_type[]
```
Example:
```sql
INTEGER[], TEXT[], BOOLEAN[]
```

#### Declaring Arrays in Tables  
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name TEXT,
    roles TEXT[]  -- Array of text values
);
```

#### Inserting Data  
```sql
INSERT INTO users (name, roles) 
VALUES ('Alice', ARRAY['admin', 'editor']);
```

#### Retrieving Data  
| Query | Example |
|-------|---------|
| Retrieve full array | `SELECT roles FROM users;` |
| Retrieve specific element (1-based index) | `SELECT roles[1] FROM users;` |
| Retrieve all rows where array contains a value | `SELECT * FROM users WHERE 'admin' = ANY(roles);` |

#### Modifying Arrays  
| Operation | Query |
|-----------|-------|
| Append an element | `UPDATE users SET roles = array_append(roles, 'moderator') WHERE name = 'Alice';` |
| Remove an element | `UPDATE users SET roles = array_remove(roles, 'editor') WHERE name = 'Alice';` |
| Concatenate two arrays | `SELECT ARRAY[1,2,3] || ARRAY[4,5];` |

#### Searching in Arrays  
- Check if a value exists in an array:  
  ```sql
  SELECT * FROM users WHERE roles @> ARRAY['admin'];  -- roles contains 'admin'
  ```

#### When to Use Arrays  
| Scenario | Recommended? | Alternative |
|----------|-------------|-------------|
| Storing a list of tags or labels | ✅ Yes | - |
| Storing structured, searchable data | ❌ No | Use `JSONB` or a separate table |
| Many-to-many relationships | ❌ No | Use a junction table |

---