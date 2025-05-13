## 🧑‍⚖️ **SQL MERGE Statement**

### 1. **Basic MERGE Syntax**

```sql
-- Trick: Basic MERGE for inserting, updating, or deleting data in one step
MERGE INTO target_table AS target
USING source_table AS source
ON target.id = source.id
WHEN MATCHED THEN
    UPDATE SET target.name = source.name
WHEN NOT MATCHED THEN
    INSERT (id, name) VALUES (source.id, source.name)
WHEN NOT MATCHED BY SOURCE THEN
    DELETE;
```

**Use when**: You need to perform conditional `INSERT`, `UPDATE`, or `DELETE` operations in a single query based on whether rows match.

---

### 2. **MERGE with Conditional Updates**

```sql
-- Trick: MERGE with different actions based on matching data
MERGE INTO employees AS target
USING new_salaries AS source
ON target.employee_id = source.employee_id
WHEN MATCHED AND source.salary > target.salary THEN
    UPDATE SET target.salary = source.salary
WHEN NOT MATCHED THEN
    INSERT (employee_id, salary) VALUES (source.employee_id, source.salary);
```

**Use when**: You need to conditionally update data, for example, updating only if the new value is greater than the existing one.

---

### 3. **MERGE with Multiple Actions**

```sql
-- Trick: MERGE with multiple conditional actions
MERGE INTO products AS target
USING new_products AS source
ON target.product_id = source.product_id
WHEN MATCHED AND source.stock < 10 THEN
    UPDATE SET target.status = 'Reorder'
WHEN MATCHED AND source.stock >= 10 THEN
    UPDATE SET target.status = 'In Stock'
WHEN NOT MATCHED THEN
    INSERT (product_id, product_name, stock, status)
    VALUES (source.product_id, source.product_name, source.stock, 'New');
```

**Use when**: You want different actions for matched rows based on additional conditions.

---

### 4. **MERGE for Deleting Data**

```sql
-- Trick: MERGE to delete unmatched rows in the target table
MERGE INTO target_table AS target
USING source_table AS source
ON target.id = source.id
WHEN NOT MATCHED BY SOURCE THEN
    DELETE;
```

**Use when**: You want to delete rows in the target table that don't have corresponding rows in the source table.

---

### 5. **MERGE with Data Transformation**

```sql
-- Trick: MERGE with transformation during UPDATE
MERGE INTO employees AS target
USING new_employees AS source
ON target.employee_id = source.employee_id
WHEN MATCHED THEN
    UPDATE SET target.salary = target.salary * 1.1;  -- Applying a 10% salary increase
```

**Use when**: You want to apply transformations like calculations (e.g., salary increment) during the update.

---

### 6. **MERGE for Data Synchronization**

```sql
-- Trick: Synchronize data between two tables with MERGE
MERGE INTO target_table AS target
USING source_table AS source
ON target.id = source.id
WHEN MATCHED THEN
    UPDATE SET target.data = source.data
WHEN NOT MATCHED THEN
    INSERT (id, data) VALUES (source.id, source.data);
```

**Use when**: You want to synchronize data between two tables, ensuring both have the same rows.

---

### 7. **MERGE with Complex Conditions**

```sql
-- Trick: Use MERGE with complex conditions to handle multiple actions
MERGE INTO orders AS target
USING incoming_orders AS source
ON target.order_id = source.order_id
WHEN MATCHED AND source.status = 'Shipped' THEN
    UPDATE SET target.shipped_date = CURRENT_DATE
WHEN MATCHED AND source.status = 'Canceled' THEN
    DELETE
WHEN NOT MATCHED THEN
    INSERT (order_id, product_id, quantity, status)
    VALUES (source.order_id, source.product_id, source.quantity, source.status);
```

**Use when**: You need to perform different actions like `UPDATE`, `DELETE`, and `INSERT` based on multiple conditions.

---

### 8. **MERGE with Joins**

```sql
-- Trick: Merge using multiple tables (Join-based)
MERGE INTO target_table AS target
USING (SELECT s.id, s.name, t.status FROM source_table s JOIN target_table t ON s.id = t.id) AS source
ON target.id = source.id
WHEN MATCHED THEN
    UPDATE SET target.status = source.status
WHEN NOT MATCHED THEN
    INSERT (id, name, status) VALUES (source.id, source.name, source.status);
```

**Use when**: You need to merge data from multiple tables (using joins) before performing insert or update operations.

---

### 9. **MERGE for Conditional Insert Only**

```sql
-- Trick: MERGE to only insert data when no match is found
MERGE INTO target_table AS target
USING source_table AS source
ON target.id = source.id
WHEN NOT MATCHED THEN
    INSERT (id, name) VALUES (source.id, source.name);
```

**Use when**: You only want to insert new data where no matching rows exist in the target table.

---

### 10. **MERGE with Transaction Control**

```sql
-- Trick: Use MERGE inside a transaction for atomic operations
BEGIN TRANSACTION;
MERGE INTO target_table AS target
USING source_table AS source
ON target.id = source.id
WHEN MATCHED THEN
    UPDATE SET target.data = source.data
WHEN NOT MATCHED THEN
    INSERT (id, data) VALUES (source.id, source.data);
COMMIT;
```

**Use when**: You want to ensure that the `MERGE` operation is atomic and can be rolled back if something goes wrong.

---

### 11. **MERGE with Null Handling**

```sql
-- Trick: Handle NULLs during MERGE operations
MERGE INTO employees AS target
USING new_salaries AS source
ON target.employee_id = source.employee_id
WHEN MATCHED AND source.salary IS NOT NULL THEN
    UPDATE SET target.salary = source.salary
WHEN NOT MATCHED THEN
    INSERT (employee_id, salary) VALUES (source.employee_id, 0);  -- Insert 0 if NULL
```

**Use when**: You want to handle `NULL` values properly during the `MERGE` operation (e.g., insert a default value for `NULL`).

---

### 12. **MERGE with OUTPUT Clause**

```sql
-- Trick: Use the OUTPUT clause to see what was changed
MERGE INTO employees AS target
USING new_salaries AS source
ON target.employee_id = source.employee_id
WHEN MATCHED THEN
    UPDATE SET target.salary = source.salary
OUTPUT inserted.employee_id, inserted.salary, deleted.salary;
```

**Use when**: You want to capture and examine what changes were made during the `MERGE`.

---

### 13. **MERGE with Identity Columns**

```sql
-- Trick: Use MERGE with identity columns for automatic ID generation
MERGE INTO products AS target
USING new_products AS source
ON target.product_code = source.product_code
WHEN NOT MATCHED THEN
    INSERT (product_code, product_name) 
    VALUES (source.product_code, source.product_name);
```

**Use when**: You want the database to auto-generate IDs (typically for identity columns) while performing the `MERGE`.

---

### 14. **MERGE for Bulk Data Update/Insert**

```sql
-- Trick: Use MERGE to efficiently update or insert large volumes of data
MERGE INTO target_table AS target
USING source_table AS source
ON target.id = source.id
WHEN MATCHED THEN
    UPDATE SET target.name = source.name, target.salary = source.salary
WHEN NOT MATCHED THEN
    INSERT (id, name, salary) VALUES (source.id, source.name, source.salary);
```

**Use when**: You need to update or insert large amounts of data in one operation for efficiency.

---

### Key Tips for MERGE:

* **MERGE** can be very useful in **ETL** (Extract, Transform, Load) operations and data synchronization tasks.
* **NULL Handling** is crucial to ensure that NULL values don't lead to incorrect updates or inserts.
* Use **transactions** to ensure that the **MERGE** operation is atomic and reversible.
* For **complex matching**, you can use **Joins** inside the **MERGE** statement to merge from multiple tables.

---
