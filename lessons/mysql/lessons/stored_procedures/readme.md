## Stored Procedures

A **stored procedure** is a group of SQL statements stored in the database that can be executed as a single unit. It encapsulates logic for tasks such as validation, transformation, and batch processing.

---

### Features

* Resides in the database and reduces network traffic.
* Encapsulates business logic and ensures reuse.
* Accepts parameters (`IN`, `OUT`, `INOUT`) for input and output.
* Supports control flow (conditional statements, loops).
* Allows declaring variables and error handlers.

---

### Syntax

```sql
DELIMITER $$

CREATE PROCEDURE procedure_name (
    IN in_param datatype,
    OUT out_param datatype,
    INOUT inout_param datatype
)
BEGIN
    -- SQL statements
END$$

DELIMITER ;
```

---

### Example

```sql
DELIMITER $$

CREATE PROCEDURE GetDiscount (
    IN original_price DECIMAL(10,2),
    OUT final_price DECIMAL(10,2)
)
BEGIN
    SET final_price = original_price * 0.90;
END$$

DELIMITER ;

-- Call it
CALL GetDiscount(100.00, @result);
SELECT @result;
```

---

### Parameter Modes

| Mode    | Description                          |
| ------- | ------------------------------------ |
| `IN`    | Receives input from the caller       |
| `OUT`   | Sends output to the caller           |
| `INOUT` | Both receives input and sends output |

---

### Control Flow Inside Procedures

| Structure | Description                                |
| --------- | ------------------------------------------ |
| `IF`      | Conditional branching                      |
| `CASE`    | Multi-condition branching                  |
| `LOOP`    | Infinite loop unless exited                |
| `WHILE`   | Loop with condition at the beginning       |
| `REPEAT`  | Loop with condition at the end             |
| `LEAVE`   | Exits a loop                               |
| `ITERATE` | Skips current iteration and continues loop |

---

### Variable Declaration

```sql
DECLARE variable_name datatype [DEFAULT value];
```

---

### Error Handling

```sql
DECLARE handler_type HANDLER FOR condition
    statement;
```

Example:

```sql
DECLARE CONTINUE HANDLER FOR SQLEXCEPTION
    SET @err = 'Error occurred';
```

---

### Managing Procedures

| Action          | Syntax                                        |
| --------------- | --------------------------------------------- |
| Show All        | `SHOW PROCEDURE STATUS WHERE Db = 'your_db';` |
| View Definition | `SHOW CREATE PROCEDURE procedure_name;`       |
| Drop Procedure  | `DROP PROCEDURE IF EXISTS procedure_name;`    |

---

### Benefits

* Improved performance by reducing multiple round trips.
* Promotes modular and reusable code.
* Enhances security by restricting direct access to data.
* Simplifies complex operations.

---

### Usage Scenarios

* Validating and transforming input before insertion.
* Encapsulating business rules and conditional logic.
* Repeating operations like calculations and aggregations.
* Batch updates, inserts, or clean-up tasks.

---
