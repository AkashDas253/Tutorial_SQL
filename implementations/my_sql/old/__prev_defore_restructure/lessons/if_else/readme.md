## `IF/ELSE` in MySQL

MySQL supports conditional logic using the `IF`, `IF...THEN...ELSE`, and `IF...THEN...ELSEIF...ELSE...END IF` constructs **inside stored routines** (procedures, functions, triggers, and events).

---

### Syntax

#### 1. Simple IF

```sql
IF condition THEN
   statements;
END IF;
```

#### 2. IF...ELSE

```sql
IF condition THEN
   statements;
ELSE
   alternative_statements;
END IF;
```

#### 3. IF...ELSEIF...ELSE

```sql
IF condition1 THEN
   statements1;
ELSEIF condition2 THEN
   statements2;
ELSE
   statements3;
END IF;
```

> *Note: Multiple `ELSEIF` blocks can be used.*

---

### Example: IF...ELSE in Stored Procedure

```sql
DELIMITER //
CREATE PROCEDURE check_age(IN age INT)
BEGIN
  IF age < 18 THEN
    SELECT 'Minor';
  ELSEIF age < 60 THEN
    SELECT 'Adult';
  ELSE
    SELECT 'Senior';
  END IF;
END;
//
DELIMITER ;
```

---

### Notes

| Aspect       | Details                                                            |
| ------------ | ------------------------------------------------------------------ |
| Scope        | Used inside stored procedures, functions, triggers, events         |
| Nesting      | `IF` blocks can be nested                                          |
| Alternatives | For simple cases, `IF()` function or `CASE` expression may suffice |
| Termination  | Each block must be terminated with `END IF;`                       |

---

### Comparison: IF Statement vs IF() Function

| Feature | `IF Statement`                  | `IF()` Function                         |
| ------- | ------------------------------- | --------------------------------------- |
| Usage   | Control flow inside routines    | Returns a value in a query              |
| Example | `IF condition THEN ... END IF;` | `SELECT IF(condition, value1, value2);` |
| Context | Only in stored programs         | Anywhere in SQL statements              |

---
