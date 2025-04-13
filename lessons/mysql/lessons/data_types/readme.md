## 🟦 Comprehensive Note on Data Types in MySQL

---

### ▪️ Overview

**Data types** in MySQL define the kind of data that can be stored in a column. They determine the storage space required for the data, its valid values, and operations that can be performed on it. MySQL supports a wide range of data types, including numeric, string, date/time, and binary types.

---

### ▪️ Types of Data Types in MySQL

| Category        | Data Types                                           |
|-----------------|------------------------------------------------------|
| **Numeric**     | `INT`, `BIGINT`, `FLOAT`, `DOUBLE`, `DECIMAL`        |
| **String**      | `CHAR`, `VARCHAR`, `TEXT`, `BLOB`, `ENUM`, `SET`     |
| **Date/Time**   | `DATE`, `DATETIME`, `TIMESTAMP`, `TIME`, `YEAR`      |
| **Binary**      | `BINARY`, `VARBINARY`, `BLOB`                       |
| **JSON**        | `JSON`                                               |

---

### ▪️ Numeric Data Types

| Data Type   | Description                                     | Storage       | Range                                             | Example                                      |
|-------------|-------------------------------------------------|---------------|---------------------------------------------------|----------------------------------------------|
| **INT**     | Stores integers                                 | 4 bytes       | `-2147483648` to `2147483647` (signed)           | `CREATE TABLE users (user_id INT);`          |
| **BIGINT**  | Stores large integers                           | 8 bytes       | `-9223372036854775808` to `9223372036854775807`   | `CREATE TABLE transactions (transaction_id BIGINT);` |
| **FLOAT**   | Stores single-precision floating-point numbers  | 4 bytes       | Varies by precision                              | `CREATE TABLE products (price FLOAT);`       |
| **DOUBLE**  | Stores double-precision floating-point numbers  | 8 bytes       | Varies by precision                              | `CREATE TABLE measurements (length DOUBLE);`|
| **DECIMAL** | Stores exact decimal numbers                   | Varies        | Depends on precision and scale                   | `CREATE TABLE invoices (amount DECIMAL(10,2));` |

---

### ▪️ String Data Types

| Data Type   | Description                                     | Storage         | Range                                              | Example                                      |
|-------------|-------------------------------------------------|-----------------|----------------------------------------------------|----------------------------------------------|
| **CHAR**    | Fixed-length string                             | 1 byte/char     | `CHAR(n)` with n up to 255 characters              | `CREATE TABLE products (code CHAR(10));`     |
| **VARCHAR** | Variable-length string                          | 1 byte + data size | `VARCHAR(n)` with n up to 65,535 characters        | `CREATE TABLE users (username VARCHAR(255));`|
| **TEXT**    | Long text string                                | Varies          | Up to 65,535 characters                            | `CREATE TABLE articles (content TEXT);`      |
| **BLOB**    | Binary Large Object, stores binary data         | Varies          | Up to 65,535 bytes                                 | `CREATE TABLE files (file_data BLOB);`       |
| **ENUM**    | Predefined set of values                        | 1 or 2 bytes    | Max 65535 values                                   | `CREATE TABLE users (status ENUM('active', 'inactive', 'pending'));` |
| **SET**     | Multiple values from predefined set            | 1, 2, 3, or 4 bytes | Max 64 values                                       | `CREATE TABLE users (hobbies SET('reading', 'sports', 'music'));` |

---

### ▪️ Date/Time Data Types

| Data Type     | Description                                     | Storage     | Format                          | Example                                          |
|---------------|-------------------------------------------------|-------------|---------------------------------|--------------------------------------------------|
| **DATE**      | Stores date values                              | 3 bytes     | `YYYY-MM-DD`                    | `CREATE TABLE events (event_date DATE);`         |
| **DATETIME**  | Stores date and time values                     | 8 bytes     | `YYYY-MM-DD HH:MM:SS`           | `CREATE TABLE appointments (appointment_datetime DATETIME);` |
| **TIMESTAMP** | Stores timestamp, auto-updates on record changes | 4 bytes     | `YYYY-MM-DD HH:MM:SS`           | `CREATE TABLE logs (log_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP);` |
| **TIME**      | Stores time values                              | 3 bytes     | `HH:MM:SS`                      | `CREATE TABLE work_shifts (shift_start TIME);`   |
| **YEAR**      | Stores year values                              | 1 byte      | `YYYY`                          | `CREATE TABLE products (release_year YEAR);`     |

---

### ▪️ Binary Data Types

| Data Type     | Description                                      | Storage      | Example                                      |
|---------------|--------------------------------------------------|--------------|----------------------------------------------|
| **BINARY**    | Fixed-length binary data                         | 1 byte/char  | `CREATE TABLE files (file_hash BINARY(16));`  |
| **VARBINARY** | Variable-length binary data                      | 1 byte + data size | `CREATE TABLE files (file_data VARBINARY(255));` |
| **BLOB**      | Binary Large Object, stores binary data          | Varies       | `CREATE TABLE images (image_data BLOB);`      |

---

### ▪️ JSON Data Type

| Data Type   | Description                           | Storage   | Example                                      |
|-------------|---------------------------------------|-----------|----------------------------------------------|
| **JSON**    | Stores JSON-formatted data           | Varies    | `CREATE TABLE user_profiles (profile_data JSON);` |

---

### ▪️ Choosing the Right Data Type Summary

| Data Type   | Use Case                                           | Storage Type       |
|-------------|---------------------------------------------------|--------------------|
| **INT/BIGINT** | Whole numbers (IDs, counters)                    | Numeric (integer)  |
| **FLOAT/DOUBLE** | Floating-point numbers (prices, measurements)    | Numeric (float)    |
| **DECIMAL**  | Exact decimal numbers (financial data)            | Numeric (decimal)  |
| **CHAR**     | Fixed-length strings (country codes, status codes) | String (fixed)     |
| **VARCHAR**  | Variable-length strings (usernames, email)        | String (variable)  |
| **TEXT**     | Large text blocks (articles, comments)            | String (variable)  |
| **BLOB**     | Binary data (files, images)                       | Binary (large)     |
| **ENUM**     | Limited predefined values (status, types)         | String (enum)      |
| **SET**      | Multiple values from a predefined set             | String (set)       |
| **DATE/DATETIME** | Date and time data                             | Date/Time          |
| **JSON**     | JSON-formatted data                              | JSON               |

---
