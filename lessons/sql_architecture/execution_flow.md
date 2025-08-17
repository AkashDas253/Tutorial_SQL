## **SQL Execution Flow**

### **Step-by-Step Flow**

1. **Query Submission**

   * Client/application sends SQL query to the database.
   * Connection is managed via drivers (ODBC, JDBC) or interfaces (CLI, GUI).

2. **Parsing**

   * **Parser** checks SQL syntax and semantics.
   * Generates a **parse tree** representing query structure.
   * Detects any errors before execution.

3. **Query Optimization**

   * **Logical Optimization**

     * Simplifies expressions
     * Pushes predicates closer to data
     * Unnests subqueries
   * **Physical Optimization**

     * Selects join algorithms (Nested Loop, Hash Join, Merge Join)
     * Determines index usage and access paths
     * Estimates costs using statistics (cardinality, I/O, CPU)
   * Outputs an **optimized execution plan**.

4. **Execution Plan Execution**

   * **Query Executor** interprets and executes the plan.
   * Operations include:

     * Table/Index scans
     * Joins
     * Aggregations and sorts
     * Filtering (WHERE, HAVING)
   * Uses **pipelining** or **materialization** for intermediate results.

5. **Interaction with Storage Engine**

   * Reads/writes data pages from tables and indexes.
   * Uses **buffer pool/cache** for efficient memory access.
   * Ensures consistency and durability of data.

6. **Transaction Management**

   * Ensures **ACID properties**:

     * Atomicity: Rollback on errors
     * Consistency: Constraints enforced
     * Isolation: Locks, MVCC snapshots
     * Durability: Logs written to disk
   * Handles concurrency, deadlocks, and recovery if needed.

7. **Result Construction & Return**

   * Final result set is assembled.
   * Sent back to the client/application for use.

---

### **Key Notes**

* Optimizer relies on **statistics and metadata** from storage.
* Executor interacts heavily with **buffer/cache** to reduce I/O.
* Transaction manager ensures **data integrity and isolation** during execution.
* Execution can be **pipelined** (streaming data between operators) or **materialized** (storing intermediate results).

---
