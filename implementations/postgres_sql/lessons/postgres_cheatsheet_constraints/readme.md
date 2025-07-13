## **PostgreSQL Constraints: Comprehensive Cheatsheet**  

---

### **1. Overview of Constraints**  
| Constraint | Description |
|------------|-------------|
| `PRIMARY KEY` | Ensures unique, non-null values in a column or set of columns. |
| `UNIQUE` | Ensures all values in a column or set of columns are distinct. |
| `NOT NULL` | Prevents `NULL` values in a column. |
| `CHECK` | Enforces a condition on values in a column. |
| `FOREIGN KEY` | Ensures referential integrity by linking a column to another table. |
| `DEFAULT` | Assigns a default value if none is provided. |
| `EXCLUSION` | Prevents overlapping values using operators. |

---

### **2. PRIMARY KEY Constraint**  
| Feature | Details |
|---------|---------|
| Uniqueness | Ensures each row has a unique identifier. |
| Non-nullability | Automatically includes `NOT NULL`. |
| Multi-column | Supports composite keys (`PRIMARY KEY (col1, col2)`). |

**Example:**  
```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL
);
```
---

### **3. UNIQUE Constraint**  
| Feature | Details |
|---------|---------|
| Ensures uniqueness | No two rows can have the same value in the column. |
| Allows NULLs | Unlike `PRIMARY KEY`, `NULL` values are permitted. |
| Multi-column | Can apply to multiple columns together. |

**Example:**  
```sql
CREATE TABLE users (
    email TEXT UNIQUE
);
```
**Multi-column Example:**  
```sql
CREATE TABLE students (
    first_name TEXT,
    last_name TEXT,
    UNIQUE (first_name, last_name)
);
```

---

### **4. NOT NULL Constraint**  
| Feature | Details |
|---------|---------|
| Ensures presence | Prevents `NULL` values in a column. |
| Default behavior | Often combined with `PRIMARY KEY`. |

**Example:**  
```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_name TEXT NOT NULL
);
```

---

### **5. CHECK Constraint**  
| Feature | Details |
|---------|---------|
| Custom conditions | Enforces business rules using conditions. |
| Works with any data type | Can apply to numeric, text, or boolean columns. |

**Example:**  
```sql
CREATE TABLE accounts (
    balance NUMERIC CHECK (balance >= 0)
);
```
**Multiple Conditions Example:**  
```sql
CREATE TABLE employees (
    age INT CHECK (age BETWEEN 18 AND 65)
);
```

---

### **6. FOREIGN KEY Constraint**  
| Feature | Details |
|---------|---------|
| Enforces referential integrity | Ensures values exist in the referenced table. |
| Prevents orphaned rows | Deleting a parent row can be restricted. |
| Supports cascading actions | Options: `ON DELETE CASCADE`, `ON DELETE SET NULL`, `ON DELETE RESTRICT`. |

**Example:**  
```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INT REFERENCES customers(id) ON DELETE CASCADE
);
```

---

### **7. DEFAULT Constraint**  
| Feature | Details |
|---------|---------|
| Sets default values | Assigns a value when none is provided. |

**Example:**  
```sql
CREATE TABLE employees (
    hired_on DATE DEFAULT CURRENT_DATE
);
```

---

### **8. EXCLUSION Constraint**  
| Feature | Details |
|---------|---------|
| Prevents overlapping values | Works with custom operators. |

**Example:** (Ensures time slots do not overlap)
```sql
CREATE TABLE bookings (
    room INT,
    booking_period TSTZRANGE,
    EXCLUDE USING GIST (room WITH =, booking_period WITH &&)
);
```

---

### **9. Adding Constraints to Existing Tables**  
**Adding `CHECK` Constraint:**  
```sql
ALTER TABLE employees ADD CONSTRAINT age_check CHECK (age >= 18);
```
**Adding `UNIQUE` Constraint:**  
```sql
ALTER TABLE users ADD CONSTRAINT unique_email UNIQUE (email);
```
**Adding `FOREIGN KEY` Constraint:**  
```sql
ALTER TABLE orders ADD CONSTRAINT fk_customer FOREIGN KEY (customer_id) REFERENCES customers(id);
```

---

### **10. Dropping Constraints**  
**Drop `CHECK` Constraint:**  
```sql
ALTER TABLE employees DROP CONSTRAINT age_check;
```
**Drop `UNIQUE` Constraint:**  
```sql
ALTER TABLE users DROP CONSTRAINT unique_email;
```
**Drop `FOREIGN KEY` Constraint:**  
```sql
ALTER TABLE orders DROP CONSTRAINT fk_customer;
```
