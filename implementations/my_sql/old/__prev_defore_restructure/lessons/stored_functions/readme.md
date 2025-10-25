## Stored Functions

A **Stored Function** in MySQL is a stored program that returns a single value and can be used in SQL expressions. Unlike procedures, functions are designed to compute and return a value and can be used inside `SELECT`, `WHERE`, and other clauses.

---

### Features

* Always returns a single scalar value.
* Can be used in SQL expressions like built-in functions.
* Accepts only `IN` parameters (no `OUT` or `INOUT`).
* Cannot perform transactions (`COMMIT`, `ROLLBACK` not allowed).
* Must contain a `RETURN` statement.

---

### Syntax

```sql
DELIMITER $$

CREATE FUNCTION function_name (
    param_name datatype
)
RETURNS return_datatype
DETERMINISTIC
BEGIN
    -- Declarations
    -- Logic
    RETURN value;
END$$

DELIMITER ;
```

---

### Example

```sql
DELIMITER $$

CREATE FUNCTION CalculateTax(price DECIMAL(10,2))
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    RETURN price * 0.18;
END$$

DELIMITER ;

-- Usage
SELECT CalculateTax(100); -- Returns 18
```

---

### Function Qualifiers

| Qualifier           | Purpose                                                         |
| ------------------- | --------------------------------------------------------------- |
| `RETURNS`           | Specifies the return data type                                  |
| `DETERMINISTIC`     | Declares the function always returns same result for same input |
| `NOT DETERMINISTIC` | Declares function may return different results for same input   |
| `READS SQL DATA`    | Function reads data from DB but does not modify it              |
| `MODIFIES SQL DATA` | Function may change data in the database                        |

---

### Managing Functions

| Operation       | Syntax                                       |
| --------------- | -------------------------------------------- |
| Show Functions  | `SHOW FUNCTION STATUS WHERE Db = 'your_db';` |
| View Definition | `SHOW CREATE FUNCTION function_name;`        |
| Drop Function   | `DROP FUNCTION IF EXISTS function_name;`     |

---

### Differences: Stored Procedure vs Stored Function

| Feature          | Stored Procedure                      | Stored Function                    |
| ---------------- | ------------------------------------- | ---------------------------------- |
| Return Type      | No return value (optional OUT)        | Returns a single value (mandatory) |
| Usage            | Called via `CALL`                     | Used in expressions like `SELECT`  |
| Parameters       | `IN`, `OUT`, `INOUT`                  | Only `IN`                          |
| SQL in SQL Query | Cannot use in `SELECT`, `WHERE`, etc. | Can be used in SQL expressions     |

---

### Use Cases

* Calculated fields in queries (e.g., tax, discount).
* Conditional business logic embedded in queries.
* String and numeric transformations.
* Custom data formatting or validation logic.

---
