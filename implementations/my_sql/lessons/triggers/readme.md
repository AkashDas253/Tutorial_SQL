## Triggers

A **trigger** is a database object that automatically executes predefined SQL logic **in response to specific events** on a table, such as `INSERT`, `UPDATE`, or `DELETE`. Triggers enforce data integrity, log changes, or automate actions.

---

### Trigger Characteristics

* Associated with a table.
* Fires **before or after** `INSERT`, `UPDATE`, or `DELETE`.
* Executes once for each affected row.
* Cannot return values.
* Cannot commit or roll back transactions inside a trigger.
* Cannot call `CALL` to procedures that modify the same table.

---

### Syntax

```sql
CREATE TRIGGER trigger_name
{BEFORE | AFTER} {INSERT | UPDATE | DELETE}
ON table_name
FOR EACH ROW
BEGIN
    -- Trigger body (logic)
END;
```

---

### Example: Logging Insertions

```sql
CREATE TRIGGER log_user_insert
AFTER INSERT ON users
FOR EACH ROW
BEGIN
    INSERT INTO user_logs(user_id, action, action_time)
    VALUES (NEW.id, 'INSERT', NOW());
END;
```

---

### `OLD` and `NEW` References

| Context      | `INSERT` | `UPDATE`      | `DELETE` |
| ------------ | -------- | ------------- | -------- |
| `NEW.column` | ✔        | ✔ (new value) | ✘        |
| `OLD.column` | ✘        | ✔ (old value) | ✔        |

Use `OLD` for values before change and `NEW` for values after change.

---

### Trigger Types

| Timing | Event  | Use Case Example                          |
| ------ | ------ | ----------------------------------------- |
| BEFORE | INSERT | Validate or transform input data          |
| AFTER  | INSERT | Audit logs or notify systems              |
| BEFORE | UPDATE | Enforce immutability or custom validation |
| AFTER  | UPDATE | Log changes or trigger notifications      |
| BEFORE | DELETE | Prevent delete or backup data             |
| AFTER  | DELETE | Log deletion or cascade effects           |

---

### Managing Triggers

| Operation     | Syntax / Command                       |
| ------------- | -------------------------------------- |
| Show Triggers | `SHOW TRIGGERS [FROM db_name];`        |
| Drop Trigger  | `DROP TRIGGER IF EXISTS trigger_name;` |
| Show Create   | `SHOW CREATE TRIGGER trigger_name;`    |

---

### Use Cases

* **Auditing**: Log table changes.
* **Validation**: Block invalid operations.
* **History Tracking**: Keep snapshots before change.
* **Automation**: Auto-fill computed fields or timestamps.

---

### Limitations

* No `CALL` to procedures that modify the triggering table.
* Cannot use `SELECT` statements that modify data.
* Only one trigger of each timing-event combination per table.
* Triggers can't change the table they are defined on.

---
