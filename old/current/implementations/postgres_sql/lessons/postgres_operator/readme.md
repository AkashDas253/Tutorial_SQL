### PostgreSQL Operators  

#### Overview  
Operators are symbols or keywords used to perform operations on database values. PostgreSQL supports various types of operators.
 
---

### **1. Arithmetic Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `10 - 4` | `6` |
| `*` | Multiplication | `6 * 2` | `12` |
| `/` | Division | `10 / 2` | `5` |
| `%` | Modulus (Remainder) | `10 % 3` | `1` |
| `^` | Exponentiation | `2 ^ 3` | `8` |

---

### **2. Comparison Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `=` | Equal to | `5 = 5` | `TRUE` |
| `!=` or `<>` | Not equal to | `5 != 3` | `TRUE` |
| `>` | Greater than | `10 > 5` | `TRUE` |
| `<` | Less than | `3 < 8` | `TRUE` |
| `>=` | Greater than or equal | `7 >= 7` | `TRUE` |
| `<=` | Less than or equal | `6 <= 9` | `TRUE` |

---

### **3. Logical Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `AND` | Returns `TRUE` if both conditions are `TRUE` | `TRUE AND FALSE` | `FALSE` |
| `OR` | Returns `TRUE` if at least one condition is `TRUE` | `TRUE OR FALSE` | `TRUE` |
| `NOT` | Negates a condition | `NOT TRUE` | `FALSE` |

---

### **4. Bitwise Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `&` | Bitwise AND | `5 & 3` | `1` |
| `|` | Bitwise OR | `5 | 3` | `7` |
| `#` | Bitwise XOR | `5 # 3` | `6` |
| `~` | Bitwise NOT | `~5` | `-6` |
| `<<` | Left shift | `5 << 1` | `10` |
| `>>` | Right shift | `5 >> 1` | `2` |

---

### **5. String Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `||` | Concatenation | `'Hello' || ' World'` | `'Hello World'` |
| `LIKE` | Pattern match | `'text' LIKE 't%'` | `TRUE` |
| `ILIKE` | Case-insensitive match | `'TEXT' ILIKE 't%'` | `TRUE` |
| `SIMILAR TO` | SQL regex match | `'abc' SIMILAR TO 'a%'` | `TRUE` |

---

### **6. JSON Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `->` | Get JSON object field as JSON | `json_col->'name'` | `"Alice"` |
| `->>` | Get JSON object field as text | `json_col->>'name'` | `'Alice'` |
| `#>` | Get JSON path as JSON | `json_col#>'{address, city}'` | `"New York"` |
| `#>>` | Get JSON path as text | `json_col#>>'{address, city}'` | `'New York'` |

---

### **7. Array Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `@>` | Contains | `ARRAY[1,2,3] @> ARRAY[2]` | `TRUE` |
| `<@` | Contained in | `ARRAY[2] <@ ARRAY[1,2,3]` | `TRUE` |
| `&&` | Overlap | `ARRAY[1,2,3] && ARRAY[2,4]` | `TRUE` |
| `||` | Concatenate arrays | `ARRAY[1,2] || ARRAY[3,4]` | `{1,2,3,4}` |

---

### **8. Range Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `&&` | Overlaps | `[1,5] && [3,7]` | `TRUE` |
| `@>` | Contains | `[1,10] @> [5,6]` | `TRUE` |
| `<@` | Contained in | `[5,6] <@ [1,10]` | `TRUE` |

---

### **9. Null Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `IS NULL` | Checks if value is NULL | `col IS NULL` | `TRUE` if NULL |
| `IS NOT NULL` | Checks if value is NOT NULL | `col IS NOT NULL` | `TRUE` if NOT NULL` |
| `COALESCE` | Returns first non-null value | `COALESCE(NULL, 'A', 'B')` | `'A'` |

---

### **10. Special Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `DISTINCT` | Removes duplicates | `SELECT DISTINCT col FROM table;` | Unique values |
| `IN` | Matches any in a list | `col IN (1,2,3)` | `TRUE` if `col` is 1,2, or 3 |
| `NOT IN` | Not in list | `col NOT IN (1,2,3)` | `TRUE` if not 1,2,3 |

---