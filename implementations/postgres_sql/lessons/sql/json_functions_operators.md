## PostgreSQL – JSON Functions & Operators

### Overview

PostgreSQL provides **robust support for JSON data**, enabling storage, querying, and manipulation of JSON documents. JSON support is available via **`json`** and **`jsonb`** (binary-optimized) data types. JSON functions and operators allow **flexible access, modification, and extraction** of JSON data.

### Key Concepts

* **Purpose**

  * Store and manage **semi-structured data**.
  * Query JSON data efficiently.
  * Combine relational and JSON-based queries.

* **JSON Data Types**

  * **json**

    * Stores JSON data as **text**.
    * Preserves exact input formatting.
    * Slower for querying.
  * **jsonb**

    * Stores JSON in a **binary format**.
    * Supports indexing, faster querying, and manipulation.
    * Recommended for most applications.

* **JSON Operators**

  * **->** : Get JSON object field by key (returns JSON)

    ```sql
    SELECT data -> 'name' FROM employees;
    ```
  * **->>** : Get JSON object field by key (returns text)

    ```sql
    SELECT data ->> 'name' FROM employees;
    ```
  * **#>** : Get JSON object at path (returns JSON)

    ```sql
    SELECT data #> '{address, city}' FROM employees;
    ```
  * **#>>** : Get JSON object at path (returns text)

    ```sql
    SELECT data #>> '{address, city}' FROM employees;
    ```
  * **@>** : JSON containment

    ```sql
    SELECT * FROM employees WHERE data @> '{"department":"HR"}';
    ```
  * **<@** : JSON is contained by

    ```sql
    SELECT '{"a":1}'::jsonb <@ '{"a":1,"b":2}'::jsonb;  -- true
    ```
  * **?|** : Any key exists

    ```sql
    SELECT * FROM employees WHERE data ?| array['name','salary'];
    ```
  * **?&** : All keys exist

    ```sql
    SELECT * FROM employees WHERE data ?& array['name','department'];
    ```

* **JSON Functions**

  * **json\_typeof(json)** – Returns type: `object`, `array`, `string`, etc.
  * **jsonb\_array\_length(jsonb)** – Returns length of JSON array.
  * **jsonb\_each(jsonb)** – Expands JSON object into key-value pairs.
  * **jsonb\_each\_text(jsonb)** – Expands JSON object into text key-value pairs.
  * **jsonb\_object\_keys(jsonb)** – Returns set of keys in JSON object.
  * **jsonb\_array\_elements(jsonb)** – Expands JSON array into set of elements.
  * **jsonb\_set(jsonb, path, new\_value)** – Updates JSON object at specified path.

    ```sql
    UPDATE employees
    SET data = jsonb_set(data, '{department}', '"Finance"')
    WHERE id = 1;
    ```
  * **to\_json(anyelement)** – Converts SQL value to JSON.
  * **jsonb\_build\_object / jsonb\_build\_array** – Creates JSON objects/arrays.

* **Indexing JSON Data**

  * **GIN Index** on `jsonb` improves query performance for containment operations (`@>`):

    ```sql
    CREATE INDEX idx_data ON employees USING GIN (data);
    ```

* **Considerations**

  * Use **jsonb** for efficient querying and indexing.
  * For heavy write operations, `jsonb` may require **reindexing** for optimal performance.
  * Proper use of operators and functions improves readability and efficiency.

### Summary

PostgreSQL JSON functions and operators enable **powerful semi-structured data management**:

* **Operators**: ->, ->>, #>, #>>, @>, <@, ?|, ?&
* **Functions**: json\_typeof, jsonb\_array\_length, jsonb\_each, jsonb\_set, to\_json, jsonb\_build\_object/array
* **Indexing**: GIN index on `jsonb` for fast containment queries
* Supports **querying, updating, and analytics** on JSON data efficiently

---
