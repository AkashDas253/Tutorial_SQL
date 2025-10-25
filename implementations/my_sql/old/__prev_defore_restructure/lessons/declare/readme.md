## `DECLARE` in MySQL

The `DECLARE` statement is used to **define local variables, handlers, cursors**, and **conditions** inside stored programs. It must appear **at the beginning** of a block before any other statements (except `BEGIN...END`).

---

### General Syntax

```sql
DECLARE variable_name datatype [DEFAULT value];
```

You can declare multiple variables at once:

```sql
DECLARE var1, var2 INT DEFAULT 0;
```

---

### Types of `DECLARE`

| Type          | Purpose                               | Syntax Example                                                 |
| ------------- | ------------------------------------- | -------------------------------------------------------------- |
| **Variable**  | Local variable for temporary storage  | `DECLARE counter INT DEFAULT 0;`                               |
| **Handler**   | Error/exception handling mechanism    | `DECLARE CONTINUE HANDLER FOR SQLEXCEPTION SET has_error = 1;` |
| **Cursor**    | Row-by-row access to query results    | `DECLARE cur CURSOR FOR SELECT id FROM users;`                 |
| **Condition** | Named condition for reuse in handlers | `DECLARE condition_name CONDITION FOR SQLSTATE '23000';`       |

---

### Example: Declaring Variables

```sql
DECLARE total_sales DECIMAL(10,2) DEFAULT 0.00;
```

---

### Example: Declaring and Using Cursors

```sql
DECLARE done INT DEFAULT 0;
DECLARE cur CURSOR FOR SELECT name FROM employees;
DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;
```

---

### Example: Full Stored Procedure Using `DECLARE`

```sql
DELIMITER //
CREATE PROCEDURE count_users_by_role()
BEGIN
  DECLARE role_name VARCHAR(50);
  DECLARE user_count INT;
  DECLARE done INT DEFAULT 0;
  DECLARE cur CURSOR FOR SELECT role, COUNT(*) FROM users GROUP BY role;
  DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;

  OPEN cur;
  read_loop: LOOP
    FETCH cur INTO role_name, user_count;
    IF done THEN
      LEAVE read_loop;
    END IF;
    SELECT role_name AS Role, user_count AS Users;
  END LOOP;
  CLOSE cur;
END;
//
DELIMITER ;
```

---

### Rules and Notes

* `DECLARE` statements must be **before** any SQL logic (e.g., `SET`, `SELECT`).
* Cannot be used in top-level SQL (only in stored routines, triggers, events).
* `DECLARE` scope is **limited to the block** where it is defined.
* Initialization can be done using `DEFAULT` or later using `SET`.

---
