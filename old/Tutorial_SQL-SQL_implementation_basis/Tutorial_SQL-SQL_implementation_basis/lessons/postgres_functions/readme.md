## **PostgreSQL Functions: Comprehensive Cheatsheet**  

---

## **1. Overview of Functions**  
| Feature         | Description |
|----------------|-------------|
| **Definition**  | A reusable SQL or procedural block that returns a value. |
| **Purpose**    | Encapsulates logic, improves performance, and enhances maintainability. |
| **Return Type** | Can return a single value, a table, or a void type. |
| **Usage**      | Can be used in `SELECT`, `INSERT`, `UPDATE`, and `DELETE` statements. |
| **Languages**  | Can be written in `SQL`, `PL/pgSQL`, and other procedural languages. |

---

## **2. Creating Functions**  
| Feature | Description |
|---------|-------------|
| **Can accept parameters** | Used to pass input values dynamically. |
| **Must specify return type** | Defines the type of value returned. |
| **Uses `LANGUAGE` keyword** | Specifies the language (`plpgsql`, `sql`, etc.). |

### **Basic Function Syntax**  
```sql
CREATE FUNCTION function_name(param1 TYPE, param2 TYPE) 
RETURNS return_type AS $$
BEGIN
    -- Function logic
    RETURN value;
END;
$$ LANGUAGE plpgsql;
```

### **Example: Function to Calculate Total Price**  
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

## **3. Function Types**  

### **a) Scalar Functions**  
| Feature | Description |
|---------|-------------|
| Returns a single value | Used in `SELECT` queries. |
| Can have input parameters | Takes dynamic values. |

**Example: Convert Fahrenheit to Celsius**  
```sql
CREATE FUNCTION convert_to_celsius(fahrenheit FLOAT) 
RETURNS FLOAT AS $$
BEGIN
    RETURN (fahrenheit - 32) * 5 / 9;
END;
$$ LANGUAGE plpgsql;
```
**Usage:**  
```sql
SELECT convert_to_celsius(100);
```

---

### **b) Table-Returning Functions**  
| Feature | Description |
|---------|-------------|
| Returns a table | Used like a regular table in `SELECT` queries. |

**Example: Get Users with Active Status**  
```sql
CREATE FUNCTION get_active_users() 
RETURNS TABLE(id INT, name TEXT, email TEXT) AS $$
BEGIN
    RETURN QUERY SELECT id, name, email FROM users WHERE status = 'active';
END;
$$ LANGUAGE plpgsql;
```
**Usage:**  
```sql
SELECT * FROM get_active_users();
```

---

### **c) Void Functions**  
| Feature | Description |
|---------|-------------|
| Does not return a value | Used for logging or performing operations. |

**Example: Log Activity**  
```sql
CREATE FUNCTION log_activity(user_id INT, action TEXT) 
RETURNS VOID AS $$
BEGIN
    INSERT INTO activity_log(user_id, action, timestamp) 
    VALUES (user_id, action, NOW());
END;
$$ LANGUAGE plpgsql;
```
**Usage:**  
```sql
SELECT log_activity(1, 'Logged In');
```

---

## **4. Function Parameters**  
| Parameter Type | Description |
|---------------|-------------|
| `IN` (default) | Accepts input values but does not modify them. |
| `OUT` | Returns a value without using `RETURN`. |
| `INOUT` | Acts as both input and output. |
| `VARIADIC` | Accepts a variable number of arguments. |

**Example: Function with `OUT` Parameter**  
```sql
CREATE FUNCTION get_user_info(user_id INT, OUT name TEXT, OUT email TEXT) 
AS $$
BEGIN
    SELECT users.name, users.email INTO name, email FROM users WHERE id = user_id;
END;
$$ LANGUAGE plpgsql;
```
**Usage:**  
```sql
SELECT * FROM get_user_info(1);
```

---

## **5. Dropping Functions**  
| Command | Description |
|---------|-------------|
| `DROP FUNCTION` | Removes a function. |
| `CASCADE` | Drops dependent objects as well. |

**Example:**  
```sql
DROP FUNCTION get_total_price(INT, DECIMAL);
```
