## **Table Variables (`@`) in MS SQL Server**

---

### **Overview**

A **Table Variable** is a **variable that holds an entire table** in memory, declared using the `@` prefix.
It’s used for **temporary storage of small to moderate datasets** within a batch, function, or stored procedure — similar to a temporary table, but **with more limited scope and lifetime**.

---

### **Characteristics**

* Declared with `DECLARE @variableName TABLE (...)`.
* Exists **only within the batch, stored procedure, or function** where declared.
* Automatically **dropped** when scope ends — no explicit `DROP` required.
* Data stored is **private** to the session and **cannot be shared**.
* Stored primarily **in memory**, but large datasets may spill into **tempdb**.
* Supports **PRIMARY KEY**, **UNIQUE**, and **CHECK** constraints.
* Does **not support non-clustered indexes** (except via constraints).

---

### **Syntax**

#### **Declaration**

```sql
DECLARE @Employee TABLE (
    EmpID INT PRIMARY KEY,
    EmpName NVARCHAR(100),
    DeptID INT,
    Salary DECIMAL(10, 2)
);
```

#### **Insertion**

```sql
INSERT INTO @Employee VALUES (1, 'Alice', 10, 50000.00);
INSERT INTO @Employee VALUES (2, 'Bob', 20, 60000.00);
```

#### **Selection**

```sql
SELECT * FROM @Employee WHERE DeptID = 10;
```

---

### **Scope and Lifetime**

| Context                                | Behavior                                          |
| -------------------------------------- | ------------------------------------------------- |
| **Within a batch**                     | Exists only until batch ends                      |
| **Within a stored procedure/function** | Automatically deleted on exit                     |
| **Across sessions**                    | Not accessible                                    |
| **Across procedures**                  | Not passed between procedures unless as parameter |

---

### **Performance Aspects**

* Stored primarily **in memory**, offering **fast performance** for small datasets.
* Automatically **managed by SQL Server** — no need for manual cleanup.
* SQL Server **does not maintain statistics** on table variables (up to SQL Server 2019), which can lead to **poor query plans** for large data.
* **Less recompilation overhead** compared to temporary tables.

---

### **Example: Using Table Variables**

```sql
DECLARE @TempProducts TABLE (
    ProductID INT,
    ProductName NVARCHAR(100),
    Quantity INT
);

INSERT INTO @TempProducts VALUES (1, 'Pen', 50), (2, 'Book', 30);

SELECT * FROM @TempProducts;
```

---

### **Differences Between Table Variables and Temporary Tables**

| Feature                     | Table Variable (`@`)                  | Local Temp Table (`#`)                   |
| --------------------------- | ------------------------------------- | ---------------------------------------- |
| **Storage Location**        | Primarily memory, may spill to tempdb | Always in tempdb                         |
| **Scope**                   | Batch/procedure/function              | Session/procedure                        |
| **Lifetime**                | Ends when scope ends                  | Ends when session ends                   |
| **Indexes**                 | Limited (via constraints)             | Fully supported                          |
| **Statistics**              | Not maintained (till SQL 2019)        | Maintained                               |
| **Transactions**            | Not fully transactional               | Fully transactional                      |
| **Performance**             | Faster for small sets                 | Better for large sets                    |
| **Recompilation**           | Low                                   | High (when created/dropped in procedure) |
| **Sharing across sessions** | No                                    | No                                       |
| **Cleanup**                 | Automatic                             | Automatic or manual                      |

---

### **Advantages**

* **Lightweight** and efficient for **small temporary data**.
* **No need to drop** explicitly — cleans up automatically.
* Useful inside **UDFs (User-Defined Functions)** where temp tables are not allowed.
* Lower **locking and logging overhead**.
* **Improved performance** for scalar or inline operations.

---

### **Limitations**

* No **non-clustered indexes** (only via constraints).
* Poor performance for **large datasets**.
* **No statistics** (up to SQL Server 2019) can lead to suboptimal query plans.
* **Limited DDL support** (cannot alter after declaration).
* **Cannot use triggers**.

---

### **Best Practices**

* Use **table variables for small datasets** (<1000 rows).
* Prefer **temporary tables** for large or complex joins.
* Declare **primary keys or indexes** for optimized lookups.
* Avoid using table variables inside **loops** for bulk operations.
* From **SQL Server 2019 onward**, **deferred compilation** improves performance for larger sets.

---

### **System Metadata**

Table variables are not listed in `sys.tables` or `tempdb.sys.tables`.
However, they can internally use **worktables** in `tempdb` if memory exceeds limits.

---

### **Mermaid Diagram**

```mermaid
flowchart TD;
A[DECLARE @TableVariable] --> B[Insert Data];
B --> C[Query / Use in Joins];
C --> D{Scope Ends?};
D -->|No| C;
D -->|Yes| E[Auto Drop (Memory Cleared)];
```

---
