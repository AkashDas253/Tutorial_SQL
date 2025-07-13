## **PostgreSQL Procedures: Comprehensive Cheatsheet**  

---

## **1. Overview of Procedures**  
| Feature         | Description |
|----------------|-------------|
| **Definition**  | A reusable SQL or procedural block that executes multiple SQL statements. |
| **Purpose**    | Used for executing complex operations, batch processing, and transactions. |
| **Return Type** | Does not return a value like functions. |
| **Usage**      | Cannot be used in `SELECT`, but is executed using `CALL`. |
| **Languages**  | Can be written in `PL/pgSQL`, `SQL`, or other procedural languages. |

---

## **2. Creating Procedures**  
| Feature | Description |
|---------|-------------|
| **Can accept parameters** | Allows dynamic input values. |
| **Does not return a value** | Used for executing database operations. |
| **Can contain transactions** | Supports `COMMIT` and `ROLLBACK`. |

### **Basic Procedure Syntax**  
```sql
CREATE PROCEDURE procedure_name(param1 TYPE, param2 TYPE) 
LANGUAGE plpgsql AS $$
BEGIN
    -- Procedure logic
END;
$$;
```

### **Example: Updating Account Balance**  
```sql
CREATE PROCEDURE update_balance(account_id INT, amount DECIMAL) 
LANGUAGE plpgsql AS $$
BEGIN
    UPDATE accounts SET balance = balance + amount WHERE id = account_id;
END;
$$;
```

### **Executing a Procedure**  
```sql
CALL update_balance(1, 100.00);
```

---

## **3. Procedure vs Function**  
| Feature          | Function  | Procedure |
|-----------------|-----------|-----------|
| Returns a Value | Yes       | No        |
| Used in Queries | Yes       | No        |
| Supports Transactions | No | Yes |
| Called with `SELECT` | Yes | No |
| Called with `CALL` | No | Yes |

---

## **4. Procedures with Transactions**  
| Feature | Description |
|---------|-------------|
| **Supports `COMMIT` and `ROLLBACK`** | Ensures data integrity. |
| **Can handle multiple operations** | Useful for batch processing. |

**Example: Transfer Money Between Accounts**  
```sql
CREATE PROCEDURE transfer_funds(sender INT, receiver INT, amount DECIMAL) 
LANGUAGE plpgsql AS $$
BEGIN
    BEGIN;
    UPDATE accounts SET balance = balance - amount WHERE id = sender;
    UPDATE accounts SET balance = balance + amount WHERE id = receiver;
    COMMIT;
END;
$$;
```

**Executing the Procedure:**  
```sql
CALL transfer_funds(1, 2, 500.00);
```

---

## **5. Dropping Procedures**  
| Command | Description |
|---------|-------------|
| `DROP PROCEDURE` | Removes a procedure. |
| `CASCADE` | Drops dependent objects as well. |

**Example:**  
```sql
DROP PROCEDURE update_balance(INT, DECIMAL);
```

---