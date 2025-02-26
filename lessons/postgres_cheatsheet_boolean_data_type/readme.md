## **PostgreSQL Boolean Data Type, Functions, and Operations**  

---

### **1. Boolean Data Type**  
| Data Type | Storage | Values | Notes |
|-----------|--------|--------|-------|
| `BOOLEAN` | 1 byte | `TRUE`, `FALSE`, `NULL` | Uses 1 bit but stored in a byte for efficiency |

**Valid Boolean Inputs:**  
| Input | Interpreted As |
|-------|---------------|
| `TRUE`, `'t'`, `'true'`, `'y'`, `'yes'`, `'on'`, `'1'` | `TRUE` |
| `FALSE`, `'f'`, `'false'`, `'n'`, `'no'`, `'off'`, `'0'` | `FALSE` |
| `NULL` | `NULL` |

---

### **2. Boolean Operators**  
| Operator | Description | Example | Output |
|----------|-------------|---------|--------|
| `AND` | Logical AND | `TRUE AND FALSE` | `FALSE` |
| `OR` | Logical OR | `TRUE OR FALSE` | `TRUE` |
| `NOT` | Logical NOT | `NOT TRUE` | `FALSE` |
| `=` | Equality | `TRUE = FALSE` | `FALSE` |
| `!=` or `<>` | Inequality | `TRUE != FALSE` | `TRUE` |

---

### **3. Boolean Expressions in Queries**  
```sql
SELECT * FROM users WHERE active = TRUE;
SELECT * FROM orders WHERE delivered IS NOT TRUE;
SELECT * FROM products WHERE available IS NULL;
```

---

### **4. Boolean Functions**  
| Function | Description | Example | Output |
|----------|-------------|---------|--------|
| `BOOL_AND(expression)` | Returns `TRUE` if all values are `TRUE` | `SELECT BOOL_AND(active) FROM users;` | `TRUE` or `FALSE` |
| `BOOL_OR(expression)` | Returns `TRUE` if any value is `TRUE` | `SELECT BOOL_OR(active) FROM users;` | `TRUE` or `FALSE` |
