## **Key Components Interaction**

### **Client Layer ↔ SQL Engine**

* Client submits SQL queries via interfaces (CLI, applications, BI tools).
* SQL Engine parses, optimizes, and executes queries.
* Results are returned to the client.
* Connection/session management ensures continuity and security.

---

### **Parser ↔ Optimizer**

* Parser generates the **parse tree** from the query.
* Optimizer uses the parse tree to:

  * Apply logical transformations
  * Select efficient execution strategies
  * Estimate cost using statistics from storage

---

### **Optimizer ↔ Storage Layer**

* Optimizer uses **metadata and statistics**:

  * Table sizes, column cardinality
  * Index availability
  * Data distribution and histograms
* Chooses access paths and join strategies based on storage information.

---

### **Executor ↔ Storage Engine**

* Executor performs physical operations:

  * Table scans, index lookups, joins, aggregations
* Interacts with storage engine for:

  * Reading/writing pages
  * Buffer pool management
  * Index traversal
* Executes operations according to **optimized plan**.

---

### **Transaction Manager ↔ Executor & Storage**

* Transaction manager ensures **ACID compliance**:

  * Coordinates with executor during query execution
  * Manages locks or MVCC snapshots for isolation
  * Ensures durability with write-ahead logging
* Handles **concurrency control, deadlocks, and rollback** if required.

---

### **Buffer Pool / Cache Interaction**

* Storage engine maintains buffer pool for frequently accessed data.
* Executor reads/writes through buffer, reducing disk I/O.
* Optimizer may influence caching decisions indirectly via execution plan.

---

### **Metadata & Statistics Usage**

* Storage engine maintains table/index statistics.
* Optimizer uses this data for:

  * Cardinality estimation
  * Join order selection
  * Access path determination
* Updated periodically or on demand to improve query performance.

---

### **Flow Summary**

* Client → Parser → Optimizer → Executor → Storage Engine
* Transaction Manager coordinates across Executor and Storage Engine
* Buffer pool and statistics provide support for efficiency and optimization

---
