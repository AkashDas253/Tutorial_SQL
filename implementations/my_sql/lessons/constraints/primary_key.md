

# PRIMARY KEY in MySQL

## Introduction

* `PRIMARY KEY` is a **constraint** that uniquely identifies each row in a table.
* It enforces two rules:

  * Values must be **unique**.
  * Values must be **NOT NULL**.
* Every table can have **only one PRIMARY KEY** (but it may consist of one or more columns = *composite key*).

---

## Syntax

### In CREATE TABLE

```sql
-- Column-level
CREATE TABLE table_name (
    column_name data_type PRIMARY KEY,
    column_name2 data_type
);

-- Table-level (for single or composite key)
CREATE TABLE table_name (
    column1 data_type,
    column2 data_type,
    PRIMARY KEY (column1, column2)
);
```

### In ALTER TABLE

```sql
-- Add primary key
ALTER TABLE table_name
ADD PRIMARY KEY (column_name);

-- Drop primary key
ALTER TABLE table_name
DROP PRIMARY KEY;
```

---

## Characteristics

* **Uniqueness**: No two rows can have the same primary key value.
* **Not Null**: Primary key columns cannot contain NULL values.
* **Single per table**: Only one primary key constraint per table.
* **Index creation**: Automatically creates a unique index for faster lookups.
* **Composite key**: Can span multiple columns (all together must be unique, individual columns may repeat).
* **Storage engine specific**:

  * In InnoDB, the primary key is used as the clustered index.
  * If no primary key is defined, InnoDB creates a hidden 6-byte row ID.

---

## Examples

### Example 1: Single-column primary key

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

✔ `student_id` uniquely identifies each student.

---

### Example 2: Composite primary key

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);
```

✔ A student can enroll in multiple courses, but each `(student_id, course_id)` pair must be unique.

---

### Example 3: Adding primary key later

```sql
ALTER TABLE employees
ADD PRIMARY KEY (emp_id);
```

---

### Example 4: Dropping primary key

```sql
ALTER TABLE employees
DROP PRIMARY KEY;
```

---

## Restrictions

* Only **one PRIMARY KEY** per table (but may include multiple columns).
* Primary key columns cannot allow `NULL`.
* Cannot define two different columns with `PRIMARY KEY` separately (must define in one constraint).
* Maximum key length depends on storage engine and column types.
* Composite primary key should be used carefully (can impact joins and performance).

---

## Difference with UNIQUE

| **Aspect**       | **PRIMARY KEY**                  | **UNIQUE**                                       |
| ---------------- | -------------------------------- | ------------------------------------------------ |
| Number per table | Only one                         | Multiple allowed                                 |
| NULL values      | Not allowed                      | Allowed (one per column if not composite)        |
| Index type       | Creates clustered index (InnoDB) | Creates non-clustered unique index               |
| Purpose          | Main identifier for row          | Ensure uniqueness but not necessarily identifier |

---

## Usage Scenarios

* Identifying records uniquely (e.g., employee ID, order ID, product code).
* Ensuring data integrity in relational models.
* Supporting relationships (used by **FOREIGN KEY** in other tables).
* Improving query performance through indexing.

---
