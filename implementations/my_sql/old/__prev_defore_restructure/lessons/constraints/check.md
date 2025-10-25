

# CHECK in MySQL

## Introduction

* `CHECK` is a **constraint** that enforces a condition on column values.
* Ensures that data entered into a column or row satisfies a logical expression.
* Helps maintain **data integrity** by rejecting invalid values.

---

## Syntax

### In CREATE TABLE

```sql
CREATE TABLE table_name (
    column_name data_type CHECK (condition),
    column_name2 data_type,
    CONSTRAINT constraint_name CHECK (condition)
);
```

### In ALTER TABLE

```sql
-- Add CHECK constraint
ALTER TABLE table_name
ADD CONSTRAINT constraint_name CHECK (condition);

-- Drop CHECK constraint
ALTER TABLE table_name
DROP CHECK constraint_name;
```

---

## Characteristics

* Condition must evaluate to **TRUE** for a row to be inserted/updated.
* If condition evaluates to **FALSE** → operation fails with error.
* If condition evaluates to **UNKNOWN** (e.g., involves `NULL`) → check passes (since `NULL` means no violation).
* Supported starting from **MySQL 8.0.16** (ignored in earlier versions).

---

## Examples

### Example 1: Column-level CHECK

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    age INT CHECK (age >= 18),
    salary DECIMAL(10,2) CHECK (salary > 0)
);
```

✔ Age must be at least 18.
✔ Salary must be positive.

---

### Example 2: Table-level CHECK

```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    balance DECIMAL(10,2),
    credit_limit DECIMAL(10,2),
    CONSTRAINT chk_balance CHECK (balance >= -credit_limit)
);
```

✔ Ensures balance never falls below negative credit limit.

---

### Example 3: Using ALTER to add CHECK

```sql
ALTER TABLE employees
ADD CONSTRAINT chk_age CHECK (age <= 65);
```

---

### Example 4: Dropping CHECK

```sql
ALTER TABLE employees
DROP CHECK chk_age;
```

---

## Restrictions

* **MySQL 8.0.16+ required**; in earlier versions `CHECK` is parsed but ignored.
* Cannot use **subqueries** inside `CHECK`.
* Expressions must be deterministic (no `RAND()`, `UUID()`, etc.).
* Multiple `CHECK` constraints can exist on the same table.
* Condition applies per-row (not across multiple rows).

---

## Behavior with NULL

* If the column value is `NULL`, the `CHECK` expression evaluates to **UNKNOWN**, not `FALSE`.
* Since only `FALSE` causes rejection, `NULL` values pass the check unless combined with `NOT NULL`.

Example:

```sql
CREATE TABLE products (
    price DECIMAL(10,2) CHECK (price > 0)
);
```

✔ `NULL` is allowed unless column is also `NOT NULL`.

---

## Usage Scenarios

* Validate ranges (e.g., age, salary, percentages).
* Enforce relationships (e.g., balance cannot go below credit limit).
* Prevent invalid categorical values (e.g., gender must be 'M' or 'F').
* Reduce reliance on application-side validation.

---

## Comparison with Other Constraints

| **Constraint** | **Purpose**             | **Example**                            |
| -------------- | ----------------------- | -------------------------------------- |
| `NOT NULL`     | Prevents null values    | `age INT NOT NULL`                     |
| `UNIQUE`       | Enforces unique values  | `email VARCHAR(100) UNIQUE`            |
| `DEFAULT`      | Provides fallback value | `status VARCHAR(20) DEFAULT 'Pending'` |
| `CHECK`        | Validates condition     | `age INT CHECK (age >= 18)`            |

---
