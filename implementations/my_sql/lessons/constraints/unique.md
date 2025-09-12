
# UNIQUE in MySQL

## Introduction

* `UNIQUE` is a **constraint** in MySQL that ensures all values in a column (or a set of columns) are **distinct**.
* A table can have multiple `UNIQUE` constraints.
* Unlike `PRIMARY KEY`, `UNIQUE` allows **one `NULL` value** (per column).

---

## Syntax

### In CREATE TABLE

```sql
-- Single column UNIQUE
CREATE TABLE table_name (
    column_name data_type UNIQUE,
    column_name2 data_type
);

-- Multiple columns UNIQUE (composite unique)
CREATE TABLE table_name (
    column1 data_type,
    column2 data_type,
    UNIQUE (column1, column2)
);
```

### In ALTER TABLE

```sql
-- Add unique constraint
ALTER TABLE table_name
ADD CONSTRAINT constraint_name UNIQUE (column1, column2);

-- Drop unique constraint (need index name)
ALTER TABLE table_name
DROP INDEX constraint_name;
```

---

## Characteristics

* Prevents duplicate values in a column or combination of columns.
* Automatically creates a **unique index** on the column(s).
* Allows **NULLs**, but only one per column (since `NULL` is not considered equal to another `NULL`).
* A table can have many `UNIQUE` constraints but only one `PRIMARY KEY`.
* Can be combined with `NOT NULL` to enforce both uniqueness and non-NULL.

---

## Examples

### Example 1: Single column UNIQUE

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

✔ Ensures each email is unique.

---

### Example 2: Composite UNIQUE

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    UNIQUE (student_id, course_id)
);
```

✔ A student cannot enroll in the same course twice.

---

### Example 3: Adding UNIQUE constraint later

```sql
ALTER TABLE employees
ADD CONSTRAINT unique_email UNIQUE (email);
```

---

### Example 4: Dropping UNIQUE constraint

```sql
ALTER TABLE employees
DROP INDEX unique_email;
```

✔ Must drop using the index/constraint name.

---

### Example 5: UNIQUE with NOT NULL

```sql
CREATE TABLE products (
    sku VARCHAR(20) NOT NULL UNIQUE,
    name VARCHAR(100) NOT NULL
);
```

✔ Each SKU must be unique and cannot be NULL.

---

## Restrictions

* A table can have multiple `UNIQUE` constraints but only one `PRIMARY KEY`.
* Allows one `NULL` value (per column).
* Dropping requires knowing the **index name** (not just `UNIQUE`).
* Performance impact: inserts and updates check uniqueness, which may slow down large datasets.

---

## Usage Scenarios

* Enforcing unique attributes (e.g., email, username, SKU).
* Preventing duplicate records in a mapping table (via composite unique).
* Ensuring data integrity when primary key is not sufficient.

---

## Key Difference from PRIMARY KEY

| **Aspect**      | **PRIMARY KEY**              | **UNIQUE**                               |
| --------------- | ---------------------------- | ---------------------------------------- |
| Purpose         | Identifies each row uniquely | Ensures uniqueness of column/combination |
| Count per table | Only one                     | Multiple allowed                         |
| NULLs           | Not allowed                  | One NULL allowed                         |
| Index type      | Creates clustered index      | Creates unique index                     |
| Mandatory       | Always NOT NULL              | Can allow NULL unless specified NOT NULL |

---

