## Control Flow Loops in MySQL

MySQL supports three types of loop constructs for **repeated execution** of statements in stored programs:

---

### 1. `WHILE` Loop

#### Syntax

```sql
[label:] WHILE condition DO
   statements;
END WHILE [label];
```

* Evaluates `condition` **before** each iteration.
* Loop stops when condition becomes **false**.

#### Example

```sql
DECLARE x INT DEFAULT 1;
WHILE x <= 5 DO
  INSERT INTO logs(msg) VALUES (CONCAT('Log #', x));
  SET x = x + 1;
END WHILE;
```

---

### 2. `REPEAT` Loop

#### Syntax

```sql
[label:] REPEAT
   statements;
UNTIL condition
END REPEAT [label];
```

* Executes statements **first**, then evaluates condition.
* Loop stops when condition becomes **true**.

#### Example

```sql
DECLARE x INT DEFAULT 1;
REPEAT
  INSERT INTO logs(msg) VALUES (CONCAT('Repeat #', x));
  SET x = x + 1;
UNTIL x > 5
END REPEAT;
```

---

### 3. `LOOP` (Infinite unless controlled)

#### Syntax

```sql
[label:] LOOP
   statements;
   LEAVE label; -- or use ITERATE to repeat
END LOOP [label];
```

* Executes continuously unless **`LEAVE`** or **`ITERATE`** is used.
* Use for flexible control with labels.

#### Example

```sql
DECLARE x INT DEFAULT 1;
my_loop: LOOP
  IF x > 5 THEN
    LEAVE my_loop;
  END IF;
  INSERT INTO logs(msg) VALUES (CONCAT('Loop #', x));
  SET x = x + 1;
END LOOP my_loop;
```

---

### Control Statements for Loops

| Statement        | Purpose                                           |
| ---------------- | ------------------------------------------------- |
| `LEAVE label;`   | Exit from the loop immediately                    |
| `ITERATE label;` | Restart the loop from beginning (like `continue`) |

---

### Comparison Table

| Loop Type | Condition Check | Use Case                              |
| --------- | --------------- | ------------------------------------- |
| WHILE     | Before loop     | Known condition before loop           |
| REPEAT    | After loop      | Must execute at least once            |
| LOOP      | No condition    | Complex logic, use with LEAVE/ITERATE |

---
