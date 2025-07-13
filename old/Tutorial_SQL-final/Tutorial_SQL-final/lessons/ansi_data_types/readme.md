## ANSI SQL Data Types

In SQL, data types define the kind of data a column can store. Each database system may support a subset or an extension of ANSI SQL data types, but the most commonly used ones are defined below.

### **Numeric Data Types**

| **Data Type**     | **Description**                                                                 | **Example**                |  
|-------------------|---------------------------------------------------------------------------------|----------------------------|  
| **INTEGER**       | Stores whole numbers (both positive and negative).                              | `CREATE TABLE table_name (id INTEGER);` |  
| **DECIMAL**       | Stores numbers with fixed decimal points, allowing for precise calculations.    | `CREATE TABLE table_name (amount DECIMAL(10,2));` |  
| **NUMERIC**       | Similar to DECIMAL, stores fixed-point numbers with user-defined precision.    | `CREATE TABLE table_name (price NUMERIC(6,3));` |  
| **FLOAT**         | Stores approximate numeric values with floating decimal points.                 | `CREATE TABLE table_name (weight FLOAT);` |  
| **DOUBLE**        | Stores approximate numeric values with double precision (higher precision than FLOAT). | `CREATE TABLE table_name (height DOUBLE);` |  
| **SMALLINT**      | Stores small whole numbers.                                                     | `CREATE TABLE table_name (age SMALLINT);` |  
| **BIGINT**        | Stores large whole numbers.                                                     | `CREATE TABLE table_name (big_id BIGINT);` |  
| **MONEY**         | Stores currency values with fixed decimal precision.                           | `CREATE TABLE table_name (salary MONEY);` |  

---

### **Character Data Types**

| **Data Type**     | **Description**                                                                 | **Example**                |  
|-------------------|---------------------------------------------------------------------------------|----------------------------|  
| **CHAR**          | Fixed-length character string.                                                  | `CREATE TABLE table_name (code CHAR(5));` |  
| **VARCHAR**       | Variable-length character string, with a maximum length.                        | `CREATE TABLE table_name (name VARCHAR(100));` |  
| **TEXT**          | Stores long variable-length character strings (not always ANSI SQL compliant).  | `CREATE TABLE table_name (description TEXT);` |  
| **NCHAR**         | Fixed-length Unicode character string (used for internationalization).          | `CREATE TABLE table_name (name NCHAR(10));` |  
| **NVARCHAR**      | Variable-length Unicode character string.                                       | `CREATE TABLE table_name (name NVARCHAR(100));` |  
| **CLOB**          | Stores large amounts of text data (character large object).                      | `CREATE TABLE table_name (bio CLOB);` |  

---

### **Date and Time Data Types**

| **Data Type**     | **Description**                                                                 | **Example**                |  
|-------------------|---------------------------------------------------------------------------------|----------------------------|  
| **DATE**          | Stores date values (year, month, and day).                                      | `CREATE TABLE table_name (birth_date DATE);` |  
| **TIME**          | Stores time values (hours, minutes, and seconds).                               | `CREATE TABLE table_name (event_time TIME);` |  
| **TIMESTAMP**     | Stores both date and time values (year, month, day, hours, minutes, seconds).   | `CREATE TABLE table_name (created_at TIMESTAMP);` |  
| **DATETIME**      | Similar to TIMESTAMP but with different precision (some databases use this).    | `CREATE TABLE table_name (order_time DATETIME);` |  
| **INTERVAL**      | Stores a period of time (can be used for calculating differences in dates or times). | `CREATE TABLE table_name (duration INTERVAL);` |  

---

### **Boolean Data Types**

| **Data Type**     | **Description**                                                                 | **Example**                |  
|-------------------|---------------------------------------------------------------------------------|----------------------------|  
| **BOOLEAN**       | Stores boolean values, typically `TRUE` or `FALSE`.                             | `CREATE TABLE table_name (is_active BOOLEAN);` |  
| **BIT**           | Stores binary values, commonly `0` (false) or `1` (true).                       | `CREATE TABLE table_name (is_approved BIT);` |  

---

### **Binary Data Types**

| **Data Type**     | **Description**                                                                 | **Example**                |  
|-------------------|---------------------------------------------------------------------------------|----------------------------|  
| **BINARY**        | Fixed-length binary data.                                                       | `CREATE TABLE table_name (file_data BINARY(20));` |  
| **VARBINARY**     | Variable-length binary data.                                                    | `CREATE TABLE table_name (file_data VARBINARY(100));` |  
| **BLOB**          | Stores binary large objects (large data like images or files).                  | `CREATE TABLE table_name (image BLOB);` |  

---

### **UUID (Universal Unique Identifier)**

| **Data Type**     | **Description**                                                                 | **Example**                |  
|-------------------|---------------------------------------------------------------------------------|----------------------------|  
| **UUID**          | Stores globally unique identifiers.                                              | `CREATE TABLE table_name (id UUID);` |  

---

### **JSON Data Types** (Not part of ANSI SQL, but widely supported)

| **Data Type**     | **Description**                                                                 | **Example**                |  
|-------------------|---------------------------------------------------------------------------------|----------------------------|  
| **JSON**          | Stores JSON formatted data.                                                     | `CREATE TABLE table_name (data JSON);` |  
| **JSONB**         | Stores JSON formatted data in a binary format (optimized for search).           | `CREATE TABLE table_name (data JSONB);` |  

---

### **Usage Examples**

1. **Numeric Example**:  
```sql
CREATE TABLE products (
    product_id BIGINT,
    product_name VARCHAR(100),
    price DECIMAL(10, 2)
);
```

2. **Character Example**:  
```sql
CREATE TABLE users (
    user_id INT,
    user_name VARCHAR(50),
    email TEXT
);
```

3. **Date and Time Example**:  
```sql
CREATE TABLE events (
    event_id INT,
    event_date DATE,
    event_time TIME
);
```

4. **Boolean Example**:  
```sql
CREATE TABLE accounts (
    account_id INT,
    account_active BOOLEAN
);
```

5. **JSON Example**:  
```sql
CREATE TABLE settings (
    user_id INT,
    preferences JSON
);
```

---

### **Conclusion**

Understanding data types is fundamental to database design, as they ensure that data is stored in a consistent and efficient manner. ANSI SQL provides a set of basic data types, while many database management systems extend this with additional types (e.g., JSON, UUID, BLOB). Careful selection of data types based on the type of data to be stored ensures efficient querying, storage, and performance.
