## CURSOR in MySQL

A **cursor** is a pointer used to traverse over a set of rows returned by a `SELECT` query, one row at a time. Cursors are used in situations where operations need to be performed on individual rows within a stored procedure or function.

---

### Cursor Types

1. **Implicit Cursors**:

   * Automatically created when a `SELECT` statement is executed within a procedure.
   * No need for explicit `OPEN`, `FETCH`, or `CLOSE`.

2. **Explicit Cursors**:

   * Created manually by the programmer and offer more control.
   * Useful when handling complex result sets.

---

### Steps for Using Explicit Cursors

1. **Declare the Cursor**:

   * A cursor is declared with a `SELECT` statement.

   #### Syntax:

   ```sql
   DECLARE cursor_name CURSOR FOR select_statement;
   ```

   #### Example:

   ```sql
   DECLARE employee_cursor CURSOR FOR
   SELECT employee_id, name FROM employees WHERE department = 'Sales';
   ```

2. **Open the Cursor**:

   * The `OPEN` statement initializes the cursor and prepares it to fetch rows.

   #### Syntax:

   ```sql
   OPEN cursor_name;
   ```

   #### Example:

   ```sql
   OPEN employee_cursor;
   ```

3. **Fetch Rows**:

   * The `FETCH` statement retrieves a row from the cursor’s result set and stores the values in variables.

   #### Syntax:

   ```sql
   FETCH cursor_name INTO variable1, variable2, ...;
   ```

   #### Example:

   ```sql
   FETCH employee_cursor INTO @emp_id, @emp_name;
   ```

4. **Close the Cursor**:

   * The `CLOSE` statement releases the cursor after its usage.

   #### Syntax:

   ```sql
   CLOSE cursor_name;
   ```

   #### Example:

   ```sql
   CLOSE employee_cursor;
   ```

---

### Complete Example of Cursor Usage

```sql
DELIMITER $$

CREATE PROCEDURE process_employees()
BEGIN
   DECLARE done INT DEFAULT 0;
   DECLARE emp_id INT;
   DECLARE emp_name VARCHAR(100);
   DECLARE employee_cursor CURSOR FOR
       SELECT employee_id, name FROM employees WHERE department = 'Sales';
   
   DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;

   -- Open the cursor
   OPEN employee_cursor;

   -- Fetch rows from the cursor
   read_loop: LOOP
       FETCH employee_cursor INTO emp_id, emp_name;
       IF done THEN
           LEAVE read_loop;
       END IF;
       -- Process the row (example)
       INSERT INTO processed_employees(id, name) VALUES (emp_id, emp_name);
   END LOOP;

   -- Close the cursor
   CLOSE employee_cursor;
END$$

DELIMITER ;
```

---

### Cursor Handling Considerations

1. **Fetching**:

   * A `FETCH` statement retrieves the next row into the specified variables.
   * After fetching, you should check if all rows have been processed using a handler or `NOT FOUND` condition.

2. **Handlers**:

   * `NOT FOUND` handler is often used to indicate the end of a result set.

   #### Example:

   ```sql
   DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;
   ```

3. **Multiple Cursors**:

   * You can have multiple cursors in a procedure, but they must be opened, fetched, and closed separately.

4. **Performance**:

   * Cursors are slower than set-based operations (like `INSERT INTO ... SELECT`). Use them when row-by-row operations are required.

---

### Cursor Syntax Overview

| Step           | Syntax                                                 |
| -------------- | ------------------------------------------------------ |
| Declare Cursor | `DECLARE cursor_name CURSOR FOR select_statement;`     |
| Open Cursor    | `OPEN cursor_name;`                                    |
| Fetch Row      | `FETCH cursor_name INTO variable1, variable2;`         |
| Close Cursor   | `CLOSE cursor_name;`                                   |
| Handler        | `DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;` |

---

### Usage Scenarios

* **Processing large result sets**: Loop through records and perform operations such as inserting or updating one row at a time.
* **When set-based operations are impractical**: For example, when complex logic is needed for each row, or operations need to be performed in sequence.
* **For reporting or audit trails**: When individual record processing is required to log specific details in another table.

---
