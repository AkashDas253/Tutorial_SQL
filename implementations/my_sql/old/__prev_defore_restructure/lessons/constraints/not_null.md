

# NOT NULL in MySQL

## Introduction

* `NOT NULL` is a **constraint** in MySQL that ensures a column cannot have `NULL` values.
* Applied when creating or altering a table.
* Forces data integrity by requiring every row to provide a value for the column.

---

## Syntax

### In CREATE TABLE

```sql
CREATE TABLE table_name (
    column_name data_type NOT NULL,
    column_name2 data_type
);
```

### In ALTER TABLE

```sql
ALTER TABLE table_name
MODIFY column_name data_type NOT NULL;
```

### In INSERT/UPDATE

```sql
INSERT INTO table_name (column_name) VALUES ('value'); -- Must not be NULL
UPDATE table_name SET column_name = 'value' WHERE condition;
```

---

## Characteristics

* Default setting for columns is `NULL` (unless `NOT NULL` is specified).
* A `NOT NULL` column **must always have a value** when inserting or updating.
* MySQL throws an error if you attempt to insert or update with `NULL`.
* `NOT NULL` can be combined with:

  * `DEFAULT` → assigns a default value if none is provided.
  * `PRIMARY KEY` → implicitly `NOT NULL`.
  * `UNIQUE` → ensures distinct values but still requires `NOT NULL` for mandatory values.

---

## Examples

### Example 1: Defining NOT NULL column

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    dept_id INT NOT NULL
);
```

✔ Ensures every employee must have a `name` and `dept_id`.

---

### Example 2: Using DEFAULT with NOT NULL

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    status VARCHAR(20) NOT NULL DEFAULT 'Pending'
);
```

✔ If no status is given, `'Pending'` is used automatically.

---

### Example 3: Altering a column to NOT NULL

```sql
ALTER TABLE employees
MODIFY dept_id INT NOT NULL;
```

✔ Prevents `NULL` from being inserted into `dept_id`.

---

### Example 4: Attempting to insert NULL

```sql
INSERT INTO employees (emp_id, name, dept_id)
VALUES (1, NULL, 10);
-- ERROR: Column 'name' cannot be null
```

---

## Restrictions

* Cannot assign `NULL` to a `NOT NULL` column.
* If altering an existing column to `NOT NULL`, all existing rows must have non-NULL values (otherwise error).
* Unlike `DEFAULT`, `NOT NULL` does not supply a value—it just enforces presence.

---

## Usage Scenarios

* Ensuring mandatory fields (e.g., username, email, employee ID).
* Enforcing referential integrity in foreign keys.
* Preventing incomplete records in transactional systems.

---

## Key Difference from NULL

| **Aspect**  | **NULL**                                | **NOT NULL**                                             |
| ----------- | --------------------------------------- | -------------------------------------------------------- |
| Meaning     | Absence of a value                      | Value must always be present                             |
| Default     | Columns allow NULL unless restricted    | Requires explicit insertion or default                   |
| Usage       | Optional fields                         | Mandatory fields                                         |
| Constraints | Works with `UNIQUE`, `DEFAULT`, `CHECK` | Common in `PRIMARY KEY`, `FOREIGN KEY`, mandatory fields |

---
