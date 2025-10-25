

# FOREIGN KEY in MySQL

## Introduction

* `FOREIGN KEY` is a **referential constraint** that links a column (or group of columns) in one table to the **PRIMARY KEY** (or `UNIQUE` key) in another table.
* Ensures **referential integrity**: values in the foreign key column must exist in the parent table.
* Prevents invalid references and maintains consistency between related tables.

---

## Syntax

### In CREATE TABLE

```sql
CREATE TABLE child_table (
    column_name data_type,
    ...
    FOREIGN KEY (column_name) REFERENCES parent_table (parent_column)
        ON DELETE action
        ON UPDATE action
);
```

### In ALTER TABLE

```sql
-- Add foreign key
ALTER TABLE child_table
ADD CONSTRAINT fk_name
FOREIGN KEY (column_name)
REFERENCES parent_table (parent_column)
ON DELETE action
ON UPDATE action;

-- Drop foreign key
ALTER TABLE child_table
DROP FOREIGN KEY fk_name;
```

---

## Characteristics

* Must reference a column in another table that is **PRIMARY KEY** or **UNIQUE**.
* Both referencing and referenced columns must have the **same data type** (or compatible).
* Foreign keys are supported in **InnoDB** (not in MyISAM).
* MySQL automatically creates an **index** on the foreign key column (if not already indexed).

---

## Referential Actions

When referenced row in **parent table** is updated or deleted, MySQL enforces rules:

| **Action**           | **ON DELETE / ON UPDATE Behavior**                                             |
| -------------------- | ------------------------------------------------------------------------------ |
| `RESTRICT` (default) | Rejects the delete/update if related rows exist in child table                 |
| `CASCADE`            | Propagates the delete/update to child table (removes/updates related rows)     |
| `SET NULL`           | Sets foreign key column to `NULL` if parent row is deleted/updated             |
| `SET DEFAULT`        | Sets foreign key column to default value (not supported in MySQL, only parses) |
| `NO ACTION`          | Same as `RESTRICT` in MySQL                                                    |

---

## Examples

### Example 1: Basic foreign key

```sql
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(100)
);

CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(100),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);
```

✔ An employee must belong to a valid department.

---

### Example 2: With ON DELETE CASCADE

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
    ON DELETE CASCADE
);
```

✔ If a customer is deleted → their orders are automatically deleted.

---

### Example 3: With ON UPDATE CASCADE

```sql
CREATE TABLE payments (
    payment_id INT PRIMARY KEY,
    order_id INT,
    FOREIGN KEY (order_id) REFERENCES orders(order_id)
    ON UPDATE CASCADE
);
```

✔ If an order ID changes → the change is reflected in payments.

---

### Example 4: Adding via ALTER

```sql
ALTER TABLE employees
ADD CONSTRAINT fk_dept
FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
ON DELETE SET NULL;
```

---

## Restrictions

* Child and parent columns must have the **same type and length**.
* Parent column must be indexed (PRIMARY or UNIQUE).
* Only supported in **InnoDB** storage engine.
* Cannot reference `TEXT` or `BLOB` columns.
* Maximum of 64 foreign keys per table.
* Circular references are possible but tricky to manage.

---

## Usage Scenarios

* Modeling **one-to-many** relationships (e.g., one department → many employees).
* Ensuring **data consistency** (e.g., no order without a valid customer).
* Enforcing **cascading rules** for delete/update.
* Relational schema integrity across multiple tables.

---

## Comparison: PRIMARY KEY vs FOREIGN KEY

| **Aspect**      | **PRIMARY KEY**                    | **FOREIGN KEY**                                 |
| --------------- | ---------------------------------- | ----------------------------------------------- |
| Purpose         | Uniquely identifies row in a table | Refers to a primary/unique key in another table |
| Null allowed    | Not allowed                        | Allowed (unless explicitly `NOT NULL`)          |
| Uniqueness      | Must be unique                     | Can have duplicates                             |
| Count per table | Only one                           | Multiple allowed                                |
| Relationship    | Defines row identity               | Enforces referential integrity                  |

---
