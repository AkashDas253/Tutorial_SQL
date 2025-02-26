## **PostgreSQL Inheritance: Comprehensive Cheatsheet**  

---

## **1. Key Concepts**  
| Feature | Description |
|---------|-------------|
| **Table Inheritance** | Allows a child table to inherit columns and constraints from a parent table. |
| **Data Visibility** | Queries on the parent table return data from both parent and child tables unless `ONLY` is used. |
| **Schema Flexibility** | Child tables can have additional columns beyond those in the parent. |
| **Indexing & Constraints** | Constraints are not automatically inherited; must be explicitly defined on child tables. |

---

## **2. Creating Inherited Tables**  

### **Defining a Parent Table**  
```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    department TEXT NOT NULL
);
```

### **Creating a Child Table That Inherits from Parent**  
```sql
CREATE TABLE managers (
    bonus NUMERIC
) INHERITS (employees);
```

### **Child Table Structure**  
| Column | Type | Source |
|--------|------|--------|
| `id` | SERIAL | Inherited from `employees` |
| `name` | TEXT | Inherited from `employees` |
| `department` | TEXT | Inherited from `employees` |
| `bonus` | NUMERIC | Defined in `managers` only |

---

## **3. Querying Inherited Tables**  

| Query | Description |
|-------|-------------|
| `SELECT * FROM employees;` | Returns all records from `employees` and inherited tables. |
| `SELECT * FROM ONLY employees;` | Returns only records from `employees`, excluding inherited tables. |
| `SELECT * FROM managers;` | Returns only records from `managers`. |

---

## **4. Insert & Delete Behavior**  
| Operation | Query |
|-----------|-------|
| **Insert into Parent** | `INSERT INTO employees (name, department) VALUES ('Alice', 'HR');` |
| **Insert into Child** | `INSERT INTO managers (name, department, bonus) VALUES ('Bob', 'Finance', 5000);` |
| **Delete from Parent** | `DELETE FROM ONLY employees WHERE id = 1;` (Prevents deleting child records) |
| **Delete from Child** | `DELETE FROM managers WHERE id = 2;` |

---

## **5. Managing Constraints & Indexes**  
| Constraint | Behavior in Inheritance |
|-----------|-------------------------|
| **PRIMARY KEY** | Not inherited—must be explicitly defined in child tables. |
| **FOREIGN KEY** | Not inherited—must be explicitly defined. |
| **CHECK Constraints** | Inherited by default but can be overridden. |
| **Indexes** | Not inherited—must be created separately for child tables. |

### **Example: Adding a Unique Constraint to Child Table**  
```sql
ALTER TABLE managers ADD CONSTRAINT unique_manager UNIQUE (id);
```

---

## **6. Converting Inheritance to Partitioning**  
| Feature | Table Inheritance | Table Partitioning |
|---------|------------------|-------------------|
| **Data Storage** | Separate storage for each table. | Unified storage via partitions. |
| **Query Performance** | Requires scanning multiple tables. | Optimized for partition pruning. |
| **Indexing** | Indexes must be created per child table. | Global indexes across partitions. |
