## PostgreSQL – Datatypes

### Overview

A **datatype** in PostgreSQL defines the **type of data that can be stored in a column or variable**. Datatypes enforce **storage format, valid values, and operations** allowed on the data. PostgreSQL supports a **wide range of native and user-defined types**.

### Key Concepts

* **Categories of Datatypes**

  * **Numeric Types**

    * **Integer Types**: `smallint` (2 bytes), `integer` (4 bytes), `bigint` (8 bytes)
    * **Serial Types**: `smallserial`, `serial`, `bigserial` (auto-increment integer types)
    * **Floating-Point**: `real` (4 bytes), `double precision` (8 bytes)
    * **Arbitrary Precision**: `numeric`, `decimal` (user-defined precision)
  * **Character Types**

    * `char(n)` – Fixed-length character string
    * `varchar(n)` – Variable-length character string with limit
    * `text` – Variable-length string without limit
    * `citext` (extension) – Case-insensitive text
  * **Boolean**

    * `boolean` – `TRUE`, `FALSE`, or `NULL`
  * **Date/Time Types**

    * `date` – Calendar date
    * `time [without time zone]` – Time of day
    * `timestamp [without time zone]` – Date and time
    * `timestamptz` – Timestamp with time zone
    * `interval` – Duration between dates/times
  * **Monetary**

    * `money` – Currency amounts
  * **UUID**

    * `uuid` – Universally unique identifier
  * **Array**

    * Any datatype can be defined as an array: `integer[]`, `text[]`
  * **JSON / JSONB**

    * `json` – Text-based JSON storage
    * `jsonb` – Binary JSON for efficient indexing and querying
  * **Hstore**

    * Key-value pair storage (`hstore` extension)
  * **Network Address Types**

    * `inet`, `cidr`, `macaddr`
  * **Range Types**

    * `int4range`, `numrange`, `tsrange`, etc.
    * Represent continuous ranges for numbers, dates, or timestamps
  * **Geometric Types**

    * `point`, `line`, `lseg`, `box`, `circle`, `polygon`, `path`
  * **Enumerated (ENUM)**

    * Predefined set of ordered values
  * **Composite Types**

    * Custom grouping of multiple fields into a single type
  * **Domain Types**

    * User-defined types with constraints
  * **Object Identifier (OID)**

    * Internal system identifier

* **Type Modifiers**

  * Length or precision for character, numeric, or timestamp types.
  * Optional `NOT NULL` constraint.

* **Casting and Conversion**

  * `CAST(expression AS target_type)` or `expression::target_type`
  * PostgreSQL supports **explicit and implicit casting** between compatible types.

* **Considerations**

  * Choosing the right type impacts **storage efficiency, performance, and precision**.
  * Use **native types** whenever possible for optimal performance.
  * Extensions may provide additional specialized types (e.g., `PostGIS` for spatial data).

### Summary

Datatypes in PostgreSQL define the **structure, format, and allowed operations** for data:

* Categories: numeric, character, boolean, date/time, arrays, JSON, UUID, ranges, geometric, enumerated, composite, domain
* Proper selection ensures **data integrity, efficient storage, and query performance**
* Supports both **built-in and user-defined types** for flexibility

---
