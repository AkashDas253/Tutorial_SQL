## Data Manipulation Language (DML) in MySQL

---

### ▪️ Overview

**Data Manipulation Language (DML)** refers to SQL commands used to **access and modify data** stored in MySQL tables. Unlike DDL, DML operations **affect the data**, not the schema. These commands are **transactional**, meaning they can be rolled back or committed based on the application's logic.

---

### ▪️ Key DML Commands

| Command   | Purpose                                           |
|-----------|---------------------------------------------------|
| `SELECT`  | Retrieve data from one or more tables              |
| `INSERT`  | Add new records to a table                         |
| `UPDATE`  | Modify existing records in a table                 |
| `DELETE`  | Remove records from a table                        |

---

### ▪️ Syntax and Usage

#### 🔹 `SELECT`
```sql
-- Basic Select
SELECT column1, column2 FROM table_name;

-- With WHERE condition
SELECT * FROM table_name WHERE condition;

-- With JOIN
SELECT a.col1, b.col2 FROM table1 a JOIN table2 b ON a.id = b.id;
```

#### 🔹 `INSERT`
```sql
-- Insert single row
INSERT INTO table_name (column1, column2) VALUES (value1, value2);

-- Insert multiple rows
INSERT INTO table_name (column1, column2)
VALUES (value1a, value2a), (value1b, value2b);

-- Insert with SELECT
INSERT INTO table2 (column1, column2)
SELECT column1, column2 FROM table1 WHERE condition;
```

#### 🔹 `UPDATE`
```sql
-- Update existing records
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```

#### 🔹 `DELETE`
```sql
-- Delete specific records
DELETE FROM table_name WHERE condition;

-- Delete all records (same as TRUNCATE but transactional)
DELETE FROM table_name;
```

---

### ▪️ Transaction Behavior

| Feature              | Description                                      |
|----------------------|--------------------------------------------------|
| **Transactional**     | DML commands can be used inside transactions     |
| **ROLLBACK possible** | Changes can be undone until `COMMIT` is issued   |
| **Locks used**        | May acquire row/table locks based on isolation   |

---

### ▪️ Clauses Commonly Used with DML

| Clause       | Applies To | Description                                      |
|--------------|------------|--------------------------------------------------|
| `WHERE`      | SELECT, UPDATE, DELETE | Filters which rows to affect        |
| `ORDER BY`   | SELECT     | Sorts the result set                             |
| `GROUP BY`   | SELECT     | Groups rows based on one or more columns         |
| `HAVING`     | SELECT     | Filters group results (used with GROUP BY)       |
| `LIMIT`      | SELECT, DELETE | Restricts number of returned/affected rows |

---

### ▪️ Performance Considerations

| Best Practice                          | Benefit                                      |
|----------------------------------------|----------------------------------------------|
| Use indexes on columns in `WHERE`      | Faster data lookup                           |
| Avoid `SELECT *`                       | Reduces unnecessary data retrieval           |
| Use batch `INSERT` for large datasets  | Improves insertion performance               |
| Always filter `DELETE`/`UPDATE`        | Prevents unintended full-table changes       |

---

### ▪️ Usage Scenarios

| Scenario                       | DML Command Used         |
|--------------------------------|---------------------------|
| Displaying user info           | `SELECT`                  |
| Adding a new customer          | `INSERT`                  |
| Changing product prices        | `UPDATE`                  |
| Deleting expired coupons       | `DELETE` with `WHERE`     |

---

### ▪️ DML vs DDL

| Feature         | DML                                | DDL                             |
|------------------|--------------------------------------|----------------------------------|
| Purpose          | Manipulates data in tables           | Defines or modifies schema       |
| Transactional    | Yes                                  | No                               |
| Affects          | Data                                 | Structure                        |
| Rollback support | Yes                                  | No                               |

---
