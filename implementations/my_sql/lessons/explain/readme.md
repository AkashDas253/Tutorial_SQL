## **EXPLAIN in MySQL**

`EXPLAIN` is used to obtain a detailed execution plan for a `SELECT`, `DELETE`, `INSERT`, `REPLACE`, or `UPDATE` statement. It provides insight into how MySQL executes queries, helping optimize performance by showing which indexes are used, how tables are joined, the order of operations, and more.

---

### **Usage of EXPLAIN**

`EXPLAIN` is placed in front of a SQL query, and it returns a result set with details about the execution plan.

#### Syntax:

```sql
EXPLAIN [EXTENDED] SELECT|DELETE|INSERT|REPLACE|UPDATE statement;
```

* `EXPLAIN EXTENDED`: Provides additional information such as rewritten query and optimization information.

#### Example:

```sql
EXPLAIN SELECT * FROM employees WHERE department = 'Sales';
```

---

### **EXPLAIN Output Columns**

1. **id**:

   * Indicates the sequence of the operation.
   * `1` is the first step, and higher numbers represent nested queries or subqueries.

2. **select\_type**:

   * Describes the type of SELECT query.

     * `SIMPLE`: No subqueries or unions.
     * `PRIMARY`: The outermost query.
     * `UNION`: Part of a union query.
     * `SUBQUERY`: A subquery in the SELECT clause.
     * `DEPENDENT SUBQUERY`: A subquery dependent on the outer query.

3. **table**:

   * Shows the table being accessed.
   * If a subquery or derived table is involved, the name of the subquery is shown.

4. **type**:

   * Indicates the join type.

     * `ALL`: Full table scan (inefficient).
     * `index`: Full index scan (faster than `ALL`).
     * `range`: Index range scan.
     * `ref`: Non-unique index lookup.
     * `eq_ref`: Unique index lookup.
     * `const`: Single row lookup (fastest).
     * `system`: System table lookup (only one row).
     * `NULL`: Not applicable.

5. **possible\_keys**:

   * Shows the indexes that could potentially be used by the query.

6. **key**:

   * Displays the index that MySQL actually used to execute the query.

7. **key\_len**:

   * Shows the length of the index key used.
   * Indicates the number of bytes MySQL uses from the index.

8. **ref**:

   * Indicates which columns or constants are being compared to the index.

9. **rows**:

   * Estimates the number of rows MySQL will examine in this step.

10. **Extra**:

    * Provides additional details:

      * `Using where`: Indicates that a WHERE clause is used to filter rows.
      * `Using index`: Means that MySQL only uses the index to satisfy the query.
      * `Using temporary`: MySQL had to create a temporary table to execute the query.
      * `Using filesort`: MySQL performed an in-memory sort (not always efficient).
      * `Using join buffer`: Indicates that MySQL used a join buffer to optimize the join.

---

### **EXPLAIN EXTENDED**

Adding `EXTENDED` gives more detailed information. The output will include a `filtered` column and show the rewritten query.

#### Example:

```sql
EXPLAIN EXTENDED SELECT * FROM employees WHERE department = 'Sales';
```

* This will show the original query and the query rewritten for optimization, including any optimizations that MySQL performed.

---

### **Example and Explanation**

```sql
EXPLAIN SELECT * FROM employees WHERE department = 'Sales';
```

| id | select\_type | table     | type | possible\_keys  | key             | key\_len | ref   | rows | Extra       |
| -- | ------------ | --------- | ---- | --------------- | --------------- | -------- | ----- | ---- | ----------- |
| 1  | SIMPLE       | employees | ref  | idx\_department | idx\_department | 4        | const | 10   | Using where |

#### Explanation:

1. **id**: `1` means it is the first (and only) step in this query.
2. **select\_type**: `SIMPLE` means no subquery is involved.
3. **table**: `employees` indicates that the query is accessing the `employees` table.
4. **type**: `ref` indicates that an index is used to search for rows.
5. **possible\_keys**: `idx_department` suggests that this index could be used.
6. **key**: `idx_department` indicates that MySQL used the `idx_department` index for this query.
7. **key\_len**: `4` indicates that MySQL used 4 bytes from the index.
8. **ref**: `const` means the query is comparing the index with a constant value (`'Sales'`).
9. **rows**: `10` indicates that MySQL expects to examine 10 rows in this step.
10. **Extra**: `Using where` means that a `WHERE` clause is being applied to filter rows.

---

### **Usage Scenarios for EXPLAIN**

1. **Index Optimization**:

   * Helps in identifying if the right indexes are being used for queries.

2. **Query Performance Tuning**:

   * By reviewing the execution plan, you can identify inefficient queries, such as those performing full table scans (`ALL` type) or requiring temporary tables (`Using temporary`).

3. **Join Optimization**:

   * Helps in understanding how different tables are being joined, and whether any join strategies (e.g., index lookups, nested loops) can be improved.

4. **Identifying Bottlenecks**:

   * By examining the `rows` and `Extra` columns, you can determine if certain parts of the query can be optimized for faster execution.

---

### **Advanced Example**

```sql
EXPLAIN SELECT * FROM orders
JOIN customers ON orders.customer_id = customers.customer_id
WHERE customers.status = 'Active';
```

| id | select\_type | table     | type | possible\_keys | key          | key\_len | ref                       | rows | Extra                 |
| -- | ------------ | --------- | ---- | -------------- | ------------ | -------- | ------------------------- | ---- | --------------------- |
| 1  | SIMPLE       | customers | ref  | PRIMARY        | PRIMARY      | 4        | const                     | 20   | Using where           |
| 1  | SIMPLE       | orders    | ref  | customer\_id   | customer\_id | 4        | db.customers.customer\_id | 100  | Using index condition |

---

### **Conclusion**

`EXPLAIN` provides a powerful tool for understanding and optimizing SQL query performance in MySQL. By analyzing the execution plan, you can identify inefficient operations, such as unnecessary full table scans, and adjust queries accordingly to use indexes or different join strategies.
