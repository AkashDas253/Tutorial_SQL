## Storage Engines in MySQL

#### Overview

A **storage engine** is the underlying software component that MySQL uses to handle SQL operations for different table types. Each engine provides different capabilities, such as support for transactions, foreign keys, locking mechanisms, and indexing techniques. You can specify the storage engine at the time of table creation using the `ENGINE` clause.

```sql
CREATE TABLE table_name (
  id INT PRIMARY KEY,
  name VARCHAR(100)
) ENGINE = InnoDB;
```

---

#### Common Storage Engines

| Engine        | Default | Transactional | Locking     | Indexing               | Foreign Keys | Use Case                            |
| ------------- | ------- | ------------- | ----------- | ---------------------- | ------------ | ----------------------------------- |
| **InnoDB**    | Yes     | Yes           | Row-level   | B-Tree, Full-text      | Yes          | General-purpose, transactional apps |
| **MyISAM**    | No      | No            | Table-level | B-Tree, Full-text      | No           | Read-heavy applications             |
| **MEMORY**    | No      | No            | Table-level | Hash                   | No           | Fast in-memory access               |
| **CSV**       | No      | No            | Table-level | None                   | No           | Data export/import in CSV format    |
| **ARCHIVE**   | No      | No            | Table-level | None (zlib-compressed) | No           | Historical data, logging            |
| **BLACKHOLE** | No      | No            | None        | None                   | No           | Replication and testing             |
| **FEDERATED** | No      | No            | Remote      | Depends on remote      | No           | Accessing remote MySQL servers      |

---

#### Detailed Storage Engine Comparison

##### 🟢 **InnoDB**

* **Default engine (MySQL 5.5 and above)**
* Supports **ACID transactions** and **row-level locking**
* Supports **foreign keys**
* **Crash recovery** and **MVCC (Multi-Version Concurrency Control)**
* Suitable for high-concurrency, write-intensive applications
* Uses a **clustered index** for primary keys

##### 🟡 **MyISAM**

* Older default engine before MySQL 5.5
* **No transaction support**
* **Table-level locking** (limits concurrent writes)
* Fast for **read-heavy** workloads
* Doesn't support **foreign keys**
* Smaller footprint but **not crash-safe**

##### 🔵 **MEMORY**

* Stores all data in **RAM** (volatile)
* Very fast, used for **temporary** or intermediate data
* Data lost on restart
* **Hash indexes** by default (can be changed to B-tree)

##### 🟠 **CSV**

* Stores data in **comma-separated text files**
* No indexing, no transactions
* Useful for **data exchange** with other systems
* Each table corresponds to `.CSV` and `.CSM` files

##### ⚪ **ARCHIVE**

* Designed for **storing large volumes** of historical data
* **Highly compressed** data, append-only
* **No indexes** (except auto-generated primary key)
* Supports only `INSERT` and `SELECT`
* Suitable for **logging**, **auditing**

##### ⚫ **BLACKHOLE**

* Accepts data but **discards it**
* No storage, no retrieval
* Used for **replication** scenarios where data is passed through but not stored
* Helps in **load testing** and debugging replication setups

##### 🔴 **FEDERATED**

* Enables **access to remote MySQL databases**
* No data stored locally
* **Acts as a proxy** table for the remote table
* Useful for **distributed** data access
* Requires setup of a `FEDERATED` table with connection info

---

#### Managing Storage Engines

* **List all available engines:**

  ```sql
  SHOW ENGINES;
  ```

* **Check default engine:**

  ```sql
  SHOW VARIABLES LIKE 'storage_engine';
  ```

* **Change engine for a table:**

  ```sql
  ALTER TABLE table_name ENGINE = InnoDB;
  ```

---

#### 🟣 PERFORMANCE\_SCHEMA

* Special-purpose **storage engine** used by MySQL for **performance monitoring and diagnostics**
* Stores **internal server execution metrics** like statement timings, wait events, stages, memory usage, etc.
* **Read-only**, cannot insert or update
* Tables reside in **memory**, not disk
* Commonly queried using:

  ```sql
  SELECT * FROM performance_schema.events_statements_summary_by_digest;
  ```
* Used by tools like **MySQL Workbench** and **performance dashboards**

---

#### Usage Scenarios

| Use Case                                               | Recommended Engine |
| ------------------------------------------------------ | ------------------ |
| Transactional applications (e.g., banking, e-commerce) | InnoDB             |
| Read-heavy static data (e.g., reporting, archives)     | MyISAM or ARCHIVE  |
| Temporary or fast-access data (e.g., caching)          | MEMORY             |
| Exporting/importing CSV files                          | CSV                |
| Testing replication or ignoring writes                 | BLACKHOLE          |
| Accessing remote MySQL tables                          | FEDERATED          |

---

#### Conclusion

Choosing the right storage engine depends on your application's needs for performance, reliability, transaction support, and storage format. **InnoDB** is typically the best choice for most applications due to its balance of features and robustness, while other engines are ideal for specialized tasks like archiving, data import/export, or replication.
