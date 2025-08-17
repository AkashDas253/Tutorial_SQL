## **PostgreSQL Triggers: Comprehensive Cheatsheet**  

---

## **1. Overview of Triggers**  
| Feature         | Description |
|----------------|-------------|
| **Definition**  | A special function that automatically executes when a specified event occurs on a table. |
| **Purpose**    | Enforces business rules, maintains data integrity, logs changes, and automates tasks. |
| **Return Type** | Uses a `TRIGGER FUNCTION` that returns `TRIGGER`. |
| **Usage**      | Applied to `INSERT`, `UPDATE`, `DELETE`, or `TRUNCATE` operations. |

---

## **2. Types of Triggers**  
| Trigger Type      | Description |
|------------------|-------------|
| **BEFORE**       | Executes before the operation (can modify row values). |
| **AFTER**        | Executes after the operation (cannot modify row values). |
| **INSTEAD OF**   | Used for views to replace the triggering operation. |
| **ROW Level**    | Executes for each row affected. |
| **STATEMENT Level** | Executes once per SQL statement. |

---

## **3. Creating a Trigger Function**  
| Feature | Description |
|---------|-------------|
| **Trigger functions return `TRIGGER`** | Special type of function used by triggers. |
| **Defined using `LANGUAGE plpgsql`** | Supports procedural SQL logic. |

### **Example: Log Inserted Data**
```sql
CREATE FUNCTION log_inserted_users() 
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO user_log(user_id, action, timestamp) 
    VALUES (NEW.id, 'INSERT', NOW());
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

---

## **4. Creating a Trigger**  
| Feature | Description |
|---------|-------------|
| **`CREATE TRIGGER` statement** | Links the trigger function to a table. |
| **`BEFORE` or `AFTER` keyword** | Specifies execution timing. |

### **Example: Trigger for `AFTER INSERT`**  
```sql
CREATE TRIGGER user_insert_trigger
AFTER INSERT ON users
FOR EACH ROW
EXECUTE FUNCTION log_inserted_users();
```

---

## **5. Trigger on `UPDATE` Operations**  
| Feature | Description |
|---------|-------------|
| **Uses `OLD` and `NEW` records** | Accesses previous and updated values. |

### **Example: Log Updated Data**
```sql
CREATE FUNCTION log_updated_users() 
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO user_log(user_id, action, timestamp, old_email, new_email) 
    VALUES (NEW.id, 'UPDATE', NOW(), OLD.email, NEW.email);
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

### **Trigger for `AFTER UPDATE`**
```sql
CREATE TRIGGER user_update_trigger
AFTER UPDATE ON users
FOR EACH ROW
EXECUTE FUNCTION log_updated_users();
```

---

## **6. Trigger on `DELETE` Operations**  
| Feature | Description |
|---------|-------------|
| **Uses `OLD` record** | Accesses deleted row data. |

### **Example: Log Deleted Records**
```sql
CREATE FUNCTION log_deleted_users() 
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO user_log(user_id, action, timestamp) 
    VALUES (OLD.id, 'DELETE', NOW());
    RETURN OLD;
END;
$$ LANGUAGE plpgsql;
```

### **Trigger for `AFTER DELETE`**
```sql
CREATE TRIGGER user_delete_trigger
AFTER DELETE ON users
FOR EACH ROW
EXECUTE FUNCTION log_deleted_users();
```

---

## **7. Trigger for `INSTEAD OF` on Views**  
| Feature | Description |
|---------|-------------|
| **Used for views** | Replaces default behavior with custom logic. |

### **Example: Redirect Inserts to Base Table**
```sql
CREATE FUNCTION handle_view_insert() 
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO users(id, name, email) VALUES (NEW.id, NEW.name, NEW.email);
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

### **Trigger for `INSTEAD OF INSERT` on a View**
```sql
CREATE TRIGGER view_insert_trigger
INSTEAD OF INSERT ON user_view
FOR EACH ROW
EXECUTE FUNCTION handle_view_insert();
```

---

## **8. Dropping Triggers**  
| Command | Description |
|---------|-------------|
| `DROP TRIGGER` | Removes a trigger. |
| `CASCADE` | Drops dependent objects. |

### **Example:**
```sql
DROP TRIGGER user_insert_trigger ON users;
```
