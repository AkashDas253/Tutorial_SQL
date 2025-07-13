## **PostgreSQL Functions & Procedures: Comprehensive Cheatsheet**  

---

## **1. Overview**
| Feature         | Description |
|----------------|-------------|
| **Functions**  | Return a value and can be used in SQL queries. |
| **Procedures** | Do not return a value and are used for executing multiple SQL statements. |
| **Purpose**    | Encapsulate logic, improve reusability, and maintainability. |

---

## **2. Creating Functions**
| Feature | Description |
|---------|-------------|
| **Returns a value** | Can be used in `SELECT` statements. |
| **Can have parameters** | Allows dynamic input values. |
| **Written in PL/pgSQL, SQL, or other languages** | PostgreSQL supports multiple procedural languages. |

### **Syntax**
```sql
CREATE FUNCTION function_name(param1 TYPE, param2 TYPE) 
RETURNS return_type AS $$
BEGIN
    -- Function logic
    RETURN value;
END;
$$ LANGUAGE plpgsql;
```

### **Example**
```sql
CREATE FUNCTION get_total_price(quantity INT, price DECIMAL) 
RETURNS DECIMAL AS $$
BEGIN
    RETURN quantity * price;
END;
$$ LANGUAGE plpgsql;
```

### **Calling a Function**
```sql
SELECT get_total_price(5, 20.00);
```

---

## **3. Creating Procedures**
| Feature | Description |
|---------|-------------|
| **Do not return a value** | Used for executing multiple statements. |
| **Can perform transactions** | Supports `COMMIT` and `ROLLBACK`. |

### **Syntax**
```sql
CREATE PROCEDURE procedure_name(param1 TYPE, param2 TYPE) 
LANGUAGE plpgsql AS $$
BEGIN
    -- Procedure logic
END;
$$;
```

### **Example**
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

## **4. Function vs Procedure**
| Feature          | Function  | Procedure |
|-----------------|-----------|-----------|
| Returns a Value | Yes       | No        |
| Used in Queries | Yes       | No        |
| Supports Transactions | No | Yes |
| Called with `SELECT` | Yes | No |
| Called with `CALL` | No | Yes |

---

## **5. Dropping Functions & Procedures**
| Command | Description |
|---------|-------------|
| `DROP FUNCTION` | Removes a function. |
| `DROP PROCEDURE` | Removes a procedure. |

### **Dropping a Function**
```sql
DROP FUNCTION get_total_price(INT, DECIMAL);
```

### **Dropping a Procedure**
```sql
DROP PROCEDURE update_balance(INT, DECIMAL);
```
