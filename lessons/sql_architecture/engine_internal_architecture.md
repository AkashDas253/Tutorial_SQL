## **SQL Engine Internal Architecture**

### **Parser**

* **Purpose**

  * Validates SQL syntax
  * Checks semantic correctness
* **Responsibilities**

  * Generates **parse tree** from SQL query
  * Decomposes query into logical components
  * Detects syntax and semantic errors

---

### **Query Optimizer**

* **Purpose**

  * Determines the most efficient execution plan for a query
* **Components & Techniques**

  * **Logical Optimization**

    * Simplify expressions
    * Predicate pushdown
    * Subquery unnesting
  * **Physical Optimization**

    * Select join strategies (Nested Loop, Hash Join, Merge Join)
    * Choose access paths (full table scan, index scan)
    * Decide on use of indexes
  * **Cost Estimation**

    * Cardinality estimation
    * I/O and CPU cost evaluation
* **Outputs**

  * Optimized **execution plan** for the query

---

### **Query Executor**

* **Purpose**

  * Executes the optimized query plan
* **Responsibilities**

  * Accesses storage via storage engine
  * Implements query operators: scans, joins, aggregations, sorts
  * Handles **pipelining** vs **materialization**
  * Produces the final **result set** for the client

---

### **Transaction Manager**

* **Purpose**

  * Ensures **ACID** properties and concurrency control
* **Responsibilities**

  * Atomicity: Rollback on failure
  * Consistency: Enforce constraints & triggers
  * Isolation: Locks, MVCC snapshots
  * Durability: Write-ahead logging (WAL)
  * Deadlock detection & resolution
  * Concurrency control (optimistic, pessimistic)

---

### **Storage Engine Interface**

* **Purpose**

  * Provides access to physical data storage
* **Responsibilities**

  * Read/write table and index data
  * Manage **buffer pool/cache**
  * Support **transactions and recovery**
  * Maintain indexes and physical data structures (heap, clustered tables)

---

### **Execution Flow**

1. SQL query received from client
2. **Parser** validates query → generates parse tree
3. **Optimizer** produces efficient execution plan
4. **Executor** runs the plan, interacts with **Storage Engine**
5. **Transaction Manager** ensures ACID compliance
6. Result set returned to client

---
