### PostgreSQL Constraints  

#### Overview  
Constraints in PostgreSQL enforce rules on table columns to ensure data integrity and consistency. They prevent invalid data from being inserted or updated.  

---

### **1. NOT NULL Constraint**  
- Ensures a column cannot store NULL values.  
- Applied at the column level.  

**Syntax:**  
```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL
);
```

---

### **2. UNIQUE Constraint**  
- Ensures all values in a column are unique.  
- Can be applied at the column or table level.  

**Syntax:**  
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email TEXT UNIQUE
);
```

**Multiple Columns:**  
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    first_name TEXT,
    last_name TEXT,
    UNIQUE (first_name, last_name)
);
```

---

### **3. PRIMARY KEY Constraint**  
- Combines `NOT NULL` and `UNIQUE`.  
- Ensures each row has a unique identifier.  

**Syntax:**  
```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_name TEXT NOT NULL
);
```

**Multiple Columns as Primary Key:**  
```sql
CREATE TABLE order_items (
    order_id INT,
    item_id INT,
    PRIMARY KEY (order_id, item_id)
);
```

---

### **4. FOREIGN KEY Constraint**  
- Ensures referential integrity by linking a column to another table's primary key.  
- Prevents actions that would violate the relationship.  

**Syntax:**  
```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INT REFERENCES customers(id)
);
```

**With `ON DELETE` Action:**  
```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INT REFERENCES customers(id) ON DELETE CASCADE
);
```

| Action | Description |
|--------|------------|
| `CASCADE` | Deletes related rows in child table. |
| `SET NULL` | Sets child foreign key to `NULL`. |
| `SET DEFAULT` | Sets default value for child foreign key. |
| `RESTRICT` | Prevents deletion if referenced. |

---

### **5. CHECK Constraint**  
- Validates data based on a condition.  

**Syntax:**  
```sql
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    price NUMERIC CHECK (price > 0)
);
```

**Multiple Conditions:**  
```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    age INT CHECK (age BETWEEN 18 AND 60)
);
```

---

### **6. DEFAULT Constraint**  
- Sets a default value when no value is provided.  

**Syntax:**  
```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    status TEXT DEFAULT 'Active'
);
```

---

### **7. EXCLUSION Constraint**  
- Ensures uniqueness based on a condition (for range overlaps).  

**Syntax:**  
```sql
CREATE TABLE bookings (
    id SERIAL PRIMARY KEY,
    room INT,
    period TSRANGE,
    EXCLUDE USING GIST (room WITH =, period WITH &&)
);
```

---

### **8. GENERATED Columns (Computed Constraints)**  
- Automatically generates values based on expressions.  

**Syntax:**  
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    first_name TEXT,
    last_name TEXT,
    full_name TEXT GENERATED ALWAYS AS (first_name || ' ' || last_name) STORED
);
```

---

### **Constraint Modification**  
| Action | Command |
|--------|---------|
| Add Constraint | `ALTER TABLE table_name ADD CONSTRAINT constraint_name constraint_type (column);` |
| Drop Constraint | `ALTER TABLE table_name DROP CONSTRAINT constraint_name;` |

---