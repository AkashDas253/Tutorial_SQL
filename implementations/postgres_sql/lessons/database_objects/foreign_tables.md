## PostgreSQL – Foreign Tables (FDW)

### Overview

A **foreign table** in PostgreSQL is a table that **represents data stored in an external data source**. **Foreign Data Wrappers (FDWs)** are the mechanism that allows PostgreSQL to **access and query external databases or data sources** as if they were local tables.

### Key Concepts

* **Purpose**

  * Access data from **other PostgreSQL databases**, SQL databases (MySQL, Oracle), NoSQL stores, or files.
  * Enable **federated queries** without data duplication.
  * Integrate external data into PostgreSQL queries and joins.

* **Foreign Data Wrapper (FDW)**

  * A **plugin** that defines how PostgreSQL communicates with an external data source.
  * Each external source requires a corresponding FDW (e.g., `postgres_fdw`, `mysql_fdw`, `file_fdw`).
  * FDWs handle **data mapping, translation, and access**.

* **Foreign Server**

  * Represents the **external data source**.
  * Created using `CREATE SERVER`.
  * Defines connection details like host, port, and database type.

* **User Mapping**

  * Maps a **PostgreSQL role to a user in the foreign system**.
  * Created using `CREATE USER MAPPING FOR role SERVER server_name`.
  * Includes authentication credentials (username/password).

* **Foreign Table Creation**

  * Syntax:

    ```sql
    CREATE FOREIGN TABLE table_name (
      column1 type1,
      column2 type2,
      ...
    )
    SERVER server_name
    OPTIONS (option 'value', ...);
    ```
  * Maps columns to the foreign source’s structure.
  * Options vary depending on the FDW (e.g., table name, file path, query).

* **Querying Foreign Tables**

  * Treated like normal tables in `SELECT`, `JOIN`, `INSERT`, `UPDATE`, and `DELETE`.
  * Performance depends on **pushdown capabilities** of the FDW:

    * Some FDWs allow filtering, joining, and aggregation to happen on the remote source.
    * Others fetch entire tables locally.

* **Advantages**

  * Seamless integration with **external data sources**.
  * Supports **cross-database joins** and reporting.
  * Avoids unnecessary data duplication.

* **Considerations**

  * Query performance depends on network latency and FDW capabilities.
  * Certain operations may be restricted (e.g., some updates, complex joins).
  * Requires **superuser privileges** for installing FDWs or creating foreign servers.

* **Common FDWs**

  * `postgres_fdw` – PostgreSQL to PostgreSQL.
  * `mysql_fdw` – MySQL.
  * `oracle_fdw` – Oracle.
  * `file_fdw` – CSV or flat files.
  * `mongo_fdw` – MongoDB.

### Summary

Foreign Tables with FDWs in PostgreSQL provide **federated access to external data sources**:

* Abstract external tables as local tables for querying
* Use FDWs to handle connectivity, translation, and pushdown optimizations
* Support cross-database joins, reporting, and integration without data duplication

---
