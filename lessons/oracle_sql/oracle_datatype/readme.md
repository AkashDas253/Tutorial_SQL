## SQL Data Types in Oracle SQL

### 1. **Character Data Types**  
Character data types are used to store text.

| **Data Type**   | **Description**                                                   | **Usage Example**                                           |
|-----------------|-------------------------------------------------------------------|-------------------------------------------------------------|
| `CHAR(size)`    | Stores fixed-length character strings. Size is between 1 and 2000. | `CHAR(10)` stores a string of 10 characters, padding with spaces if necessary. |
| `VARCHAR2(size)`| Stores variable-length character strings. Size is between 1 and 4000. | `VARCHAR2(50)` stores a string of up to 50 characters.       |
| `CLOB`          | Stores large text (up to 4 GB).                                   | `CLOB` is used for storing large text data such as documents. |

#### Usage Example:
```sql
CREATE TABLE employees (
    name VARCHAR2(100),
    address CLOB
);
```

### 2. **Numeric Data Types**  
Numeric data types are used for storing numbers, including both integers and floating-point numbers.

| **Data Type**   | **Description**                                                   | **Usage Example**                                           |
|-----------------|-------------------------------------------------------------------|-------------------------------------------------------------|
| `NUMBER(p,s)`   | Stores fixed or floating-point numbers. `p` is precision (total digits), and `s` is scale (digits after the decimal point). | `NUMBER(8,2)` can store a number with 8 total digits and 2 digits after the decimal point. |
| `FLOAT`         | Synonym for `NUMBER`. Often used to store approximate numeric values. | `FLOAT` can store numbers like `3.14159`.                   |
| `INTEGER`       | Synonym for `NUMBER(38)` or `NUMBER`. Used to store integer values. | `INTEGER` can store values like `100` or `-250`.             |

#### Usage Example:
```sql
CREATE TABLE product (
    price NUMBER(10,2),
    quantity INTEGER
);
```

### 3. **Date and Time Data Types**  
Date and time data types are used for storing date and time values.

| **Data Type**   | **Description**                                                   | **Usage Example**                                           |
|-----------------|-------------------------------------------------------------------|-------------------------------------------------------------|
| `DATE`          | Stores date and time values (year, month, day, hour, minute, second). | `DATE` stores `2025-01-01 12:30:00`.                        |
| `TIMESTAMP`     | Stores date and time with fractional seconds.                     | `TIMESTAMP` stores `2025-01-01 12:30:00.123456`.            |
| `TIMESTAMP WITH TIME ZONE` | Stores date, time, and time zone information.            | `TIMESTAMP WITH TIME ZONE` stores `2025-01-01 12:30:00 +02:00`. |
| `INTERVAL`      | Represents a period of time, either in years/months or days/seconds. | `INTERVAL '2' YEAR` represents two years.                   |

#### Usage Example:
```sql
CREATE TABLE events (
    event_date DATE,
    event_timestamp TIMESTAMP WITH TIME ZONE
);
```

### 4. **Large Object Data Types (LOBs)**  
LOBs are used to store large data like text, images, and videos.

| **Data Type**   | **Description**                                                   | **Usage Example**                                           |
|-----------------|-------------------------------------------------------------------|-------------------------------------------------------------|
| `BLOB`          | Stores binary large objects (e.g., images, videos).               | `BLOB` is used for storing binary data like images.         |
| `BFILE`         | Stores large binary data stored outside the database, usually in a file system. | `BFILE` stores large data from external files, such as video files. |
| `CLOB`          | Stores large character-based data, such as large text files.      | `CLOB` can store large amounts of text, like books or documents. |

#### Usage Example:
```sql
CREATE TABLE media (
    photo BLOB,
    description CLOB
);
```

### 5. **Boolean Data Types**  
Oracle SQL does not have a direct `BOOLEAN` data type for columns, but it can be simulated.

| **Data Type**   | **Description**                                                   | **Usage Example**                                           |
|-----------------|-------------------------------------------------------------------|-------------------------------------------------------------|
| `BOOLEAN`       | Not natively supported in Oracle SQL for table columns, but can be used in PL/SQL. | Use `NUMBER(1)` for representing Boolean (`1` = `TRUE`, `0` = `FALSE`). |

#### Usage Example:
```sql
CREATE TABLE users (
    is_active NUMBER(1)  -- 1 for active, 0 for inactive
);
```

### 6. **Raw Data Types**  
Raw data types are used to store binary data of fixed length.

| **Data Type**   | **Description**                                                   | **Usage Example**                                           |
|-----------------|-------------------------------------------------------------------|-------------------------------------------------------------|
| `RAW(size)`     | Stores binary data with a specified length. Size is between 1 and 2000. | `RAW(16)` stores a fixed-length binary string.              |
| `LONG RAW`      | Stores variable-length binary data.                               | `LONG RAW` is used for binary data of variable length, up to 2GB. |

#### Usage Example:
```sql
CREATE TABLE files (
    data RAW(100)
);
```

### 7. **ROWID and UROWID**  
These are unique identifiers used to refer to rows in a table.

| **Data Type**   | **Description**                                                   | **Usage Example**                                           |
|-----------------|-------------------------------------------------------------------|-------------------------------------------------------------|
| `ROWID`         | Stores a unique identifier for each row in a table.               | `ROWID` is used to quickly access rows in large tables.     |
| `UROWID`        | Stores a unique, platform-independent identifier for a row.       | `UROWID` is used to reference rows in a database in a portable manner. |

#### Usage Example:
```sql
CREATE TABLE audit_log (
    log_id ROWID,
    log_data VARCHAR2(100)
);
```

### 8. **User-Defined Data Types**  
Oracle allows users to define custom types, including objects and collections.

| **Data Type**   | **Description**                                                   | **Usage Example**                                           |
|-----------------|-------------------------------------------------------------------|-------------------------------------------------------------|
| `OBJECT`        | Allows users to define custom object types.                       | `CREATE TYPE person_obj AS OBJECT (name VARCHAR2(100), age NUMBER);` |
| `VARRAY`        | Allows users to define an array of elements of a specific type.   | `CREATE TYPE phone_numbers AS VARRAY(5) OF VARCHAR2(15);`    |
| `NESTED TABLE`  | Allows users to define a collection of items, similar to arrays.  | `CREATE TYPE phone_numbers AS TABLE OF VARCHAR2(15);`       |

#### Usage Example:
```sql
CREATE TYPE address_obj AS OBJECT (
    street VARCHAR2(100),
    city VARCHAR2(50),
    zip_code VARCHAR2(10)
);
```

### Notes:
- **Default Length**: If a length is not specified for `CHAR`, `VARCHAR2`, `RAW`, and other types, Oracle assigns default sizes (e.g., `VARCHAR2` defaults to 1 character).
- **Precision and Scale**: For `NUMBER(p,s)`, `p` refers to the total number of digits, and `s` refers to the digits after the decimal point. For example, `NUMBER(5,2)` can store values like `123.45`.
