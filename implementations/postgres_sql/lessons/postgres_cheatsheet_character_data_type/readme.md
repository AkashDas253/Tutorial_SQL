## **PostgreSQL Character Data Types, Functions, and Operations**  

---

### **1. Character Data Types**  
| Data Type | Storage | Notes |
|-----------|--------|-------|
| `CHAR(n)` | Fixed `n` bytes | Fixed-length string (padded with spaces) |
| `VARCHAR(n)` | Variable `n+1` bytes | Variable-length string with max `n` characters |
| `TEXT` | Variable | Unlimited-length string |

---

### **2. Character Operators**  
| Operator | Description | Example | Output |
|----------|-------------|---------|--------|
| `||` | Concatenation | `'Hello' || ' World'` | `Hello World` |
| `LENGTH()` | String length | `LENGTH('PostgreSQL')` | `10` |
| `SUBSTRING()` | Extract substring | `SUBSTRING('PostgreSQL' FROM 1 FOR 4)` | `Post` |
| `UPPER()` | Convert to uppercase | `UPPER('postgres')` | `POSTGRES` |
| `LOWER()` | Convert to lowercase | `LOWER('POSTGRES')` | `postgres` |
| `TRIM()` | Remove spaces | `TRIM(' PostgreSQL ')` | `PostgreSQL` |
| `LTRIM()` | Remove left spaces | `LTRIM(' PostgreSQL')` | `PostgreSQL` |
| `RTRIM()` | Remove right spaces | `RTRIM('PostgreSQL ')` | `PostgreSQL` |
| `POSITION()` | Find substring index | `POSITION('gre' IN 'PostgreSQL')` | `5` |
| `REPLACE()` | Replace substring | `REPLACE('PostgreSQL', 'SQL', 'DB')` | `PostgreDB` |
| `INITCAP()` | Capitalize words | `INITCAP('hello world')` | `Hello World` |
| `OVERLAY()` | Replace part of a string | `OVERLAY('PostgreSQL' PLACING 'DB' FROM 5 FOR 3)` | `PostDBSQL` |

---

### **3. Pattern Matching**  
| Operator | Description | Example | Matches |
|----------|-------------|---------|---------|
| `LIKE` | Simple pattern match | `WHERE name LIKE 'Jo%'` | `John, Joey` |
| `ILIKE` | Case-insensitive match | `WHERE name ILIKE 'jo%'` | `John, joey, JOAN` |
| `_` | Matches one character | `WHERE name LIKE 'J_n'` | `Jon, Jan` |
| `%` | Matches any length | `WHERE name LIKE 'J%n'` | `John, Jordan` |
| `SIMILAR TO` | Regex-like pattern | `WHERE name SIMILAR TO 'J_%'` | `John, Jack` |
| `~` | Regex match | `WHERE name ~ 'Jo.*'` | `John, Joey` |
| `~*` | Case-insensitive regex | `WHERE name ~* 'jo.*'` | `John, JOAN` |
