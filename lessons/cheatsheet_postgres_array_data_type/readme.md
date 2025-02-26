## **PostgreSQL Arrays: Data Type, Functions, and Operations**  

---

### **1. Array Data Type**  
| Feature | Description |
|---------|-------------|
| Storage | Stores multiple values in a single column |
| Declaration | `datatype[]` (e.g., `INTEGER[]`, `TEXT[]`) |
| Indexing | 1-based (starts at 1) |
| Multidimensional | Supported (`INTEGER[][]`) |

---

### **2. Creating and Inserting Arrays**  
```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name TEXT,
    scores INTEGER[]
);

INSERT INTO students (name, scores) VALUES ('Alice', ARRAY[90, 85, 88]);
```

---

### **3. Array Operators**  
| Operator | Description | Example | Output |
|----------|-------------|---------|--------|
| `{}` | Define an array | `'{1,2,3}'::INTEGER[]` | `{1,2,3}` |
| `ARRAY[]` | Explicit array creation | `ARRAY[10, 20, 30]` | `{10,20,30}` |
| `||` | Concatenation | `ARRAY[1,2] || ARRAY[3,4]` | `{1,2,3,4}` |
| `@>` | Contains | `ARRAY[1,2,3] @> ARRAY[2,3]` | `TRUE` |
| `<@` | Contained in | `ARRAY[2,3] <@ ARRAY[1,2,3]` | `TRUE` |
| `&&` | Overlaps | `ARRAY[1,2,3] && ARRAY[3,4,5]` | `TRUE` |
| `=` | Equality | `ARRAY[1,2,3] = ARRAY[1,2,3]` | `TRUE` |

---

### **4. Array Functions**  
| Function | Description | Example | Output |
|----------|-------------|---------|--------|
| `array_length(arr, dim)` | Length of array | `array_length(ARRAY[10, 20, 30], 1)` | `3` |
| `array_append(arr, value)` | Add element to end | `array_append(ARRAY[1,2], 3)` | `{1,2,3}` |
| `array_prepend(value, arr)` | Add element to start | `array_prepend(0, ARRAY[1,2])` | `{0,1,2}` |
| `array_cat(arr1, arr2)` | Concatenation | `array_cat(ARRAY[1,2], ARRAY[3,4])` | `{1,2,3,4}` |
| `unnest(arr)` | Expand array into rows | `SELECT unnest(ARRAY[10,20,30]);` | `10`, `20`, `30` |

---

### **5. Querying Arrays**  
#### **Checking If Array Contains a Value**
```sql
SELECT * FROM students WHERE scores @> ARRAY[90];
```
#### **Filtering Rows Where Any Element Matches**
```sql
SELECT * FROM students WHERE 85 = ANY(scores);
```
#### **Filtering Rows Where All Elements Match a Condition**
```sql
SELECT * FROM students WHERE 80 < ALL(scores);
```
#### **Fetching a Specific Index Value**
```sql
SELECT scores[1] FROM students;
```
#### **Updating an Array Field**
```sql
UPDATE students SET scores[2] = 95 WHERE name = 'Alice';
```
