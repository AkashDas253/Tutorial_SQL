## JSON Functions

MySQL provides a set of functions to work with JSON data types, allowing you to query, update, and manipulate JSON values in a more efficient way. Below are the most commonly used JSON functions in MySQL.

#### JSON Creation and Manipulation

| Function                                   | Description                                               |
| ------------------------------------------ | --------------------------------------------------------- |
| `JSON_OBJECT(key, value, ...)`             | Creates a JSON object from a list of key-value pairs      |
| `JSON_ARRAY(value, ...)`                   | Creates a JSON array from a list of values                |
| `JSON_QUOTE(value)`                        | Returns a JSON-encoded string of the value                |
| `JSON_ARRAY_APPEND(json_doc, path, value)` | Appends a value to the JSON array at the specified path   |
| `JSON_ARRAY_INSERT(json_doc, path, value)` | Inserts a value into the JSON array at the specified path |

```sql
SELECT JSON_OBJECT('name', 'John', 'age', 30); -- {"name": "John", "age": 30}
SELECT JSON_ARRAY('apple', 'banana', 'cherry'); -- ["apple", "banana", "cherry"]
SELECT JSON_QUOTE('Hello'); -- '"Hello"'
SELECT JSON_ARRAY_APPEND('[1, 2]', '$', 3); -- [1, 2, 3]
SELECT JSON_ARRAY_INSERT('[1, 2]', '$[1]', 0); -- [1, 0, 2]
```

#### JSON Retrieval Functions

| Function                                         | Description                                                      |
| ------------------------------------------------ | ---------------------------------------------------------------- |
| `JSON_EXTRACT(json_doc, path, ...)`              | Extracts values from a JSON document based on the specified path |
| `JSON_UNQUOTE(json_val)`                         | Removes the surrounding quotes from a JSON value                 |
| `JSON_CONTAINS(json_doc, value)`                 | Checks if the JSON document contains a specified value           |
| `JSON_CONTAINS_PATH(json_doc, one_or_all, path)` | Checks if the specified path exists within the JSON document     |
| `JSON_KEYS(json_doc)`                            | Returns all keys in a JSON object as a JSON array                |

```sql
SELECT JSON_EXTRACT('{"name": "John", "age": 30}', '$.name'); -- "John"
SELECT JSON_UNQUOTE('"Hello"'); -- Hello
SELECT JSON_CONTAINS('{"fruits": ["apple", "banana"]}', '"banana"'); -- 1 (true)
SELECT JSON_CONTAINS_PATH('{"name": "John", "age": 30}', 'one', '$.name'); -- 1 (true)
SELECT JSON_KEYS('{"name": "John", "age": 30}'); -- ["name", "age"]
```

#### JSON Modifying Functions

| Function                                   | Description                                                  |
| ------------------------------------------ | ------------------------------------------------------------ |
| `JSON_SET(json_doc, path, value, ...)`     | Sets the value of the specified path in the JSON document    |
| `JSON_INSERT(json_doc, path, value, ...)`  | Inserts the value at the specified path if it does not exist |
| `JSON_REPLACE(json_doc, path, value, ...)` | Replaces the value at the specified path                     |
| `JSON_REMOVE(json_doc, path, ...)`         | Removes the value at the specified path                      |
| `JSON_MERGE(json_doc1, json_doc2)`         | Merges two JSON documents together                           |

```sql
SELECT JSON_SET('{"name": "John"}', '$.age', 30); -- {"name": "John", "age": 30}
SELECT JSON_INSERT('{"name": "John"}', '$.age', 30); -- {"name": "John", "age": 30}
SELECT JSON_REPLACE('{"name": "John", "age": 30}', '$.age', 31); -- {"name": "John", "age": 31}
SELECT JSON_REMOVE('{"name": "John", "age": 30}', '$.age'); -- {"name": "John"}
SELECT JSON_MERGE('{"name": "John"}', '{"age": 30}'); -- {"name": "John", "age": 30}
```

#### JSON Array Functions

| Function                                     | Description                                                    |
| -------------------------------------------- | -------------------------------------------------------------- |
| `JSON_ARRAY_LENGTH(json_array)`              | Returns the length of the JSON array                           |
| `JSON_ARRAY_INSERT(json_array, path, value)` | Inserts a value into a JSON array at the specified position    |
| `JSON_ARRAY_APPEND(json_array, value)`       | Appends a value to the end of the JSON array                   |
| `JSON_EXTRACT(json_array, path)`             | Extracts a value from a JSON array based on the specified path |
| `JSON_UNQUOTE(json_array)`                   | Removes the surrounding quotes from a JSON array               |

```sql
SELECT JSON_ARRAY_LENGTH('[1, 2, 3]'); -- 3
SELECT JSON_ARRAY_INSERT('[1, 2, 3]', '$[1]', 4); -- [1, 4, 2, 3]
SELECT JSON_ARRAY_APPEND('[1, 2]', 3); -- [1, 2, 3]
SELECT JSON_EXTRACT('[1, 2, 3]', '$[1]'); -- 2
SELECT JSON_UNQUOTE('["apple"]'); -- apple
```

#### JSON Validation

| Function         | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| `IS_JSON(value)` | Returns 1 if the value is a valid JSON document, otherwise 0 |

```sql
SELECT IS_JSON('{"name": "John", "age": 30}'); -- 1
SELECT IS_JSON('Invalid JSON'); -- 0
```

---

### Usage Scenarios

* **Storing and retrieving JSON objects:**

  ```sql
  -- Store JSON object in a column
  INSERT INTO users (profile) VALUES (JSON_OBJECT('name', 'John', 'age', 30));

  -- Retrieve name from the JSON object
  SELECT JSON_EXTRACT(profile, '$.name') FROM users;
  ```

* **Appending to a JSON array:**

  ```sql
  -- Append a new element to a JSON array
  UPDATE products SET tags = JSON_ARRAY_APPEND(tags, '$', 'new_tag') WHERE id = 1;
  ```

* **Replacing JSON values:**

  ```sql
  -- Replace value in a JSON object
  UPDATE orders SET status = JSON_REPLACE(order_details, '$.status', 'Shipped') WHERE id = 1001;
  ```

* **Conditional JSON updates:**

  ```sql
  -- Conditionally update a value in the JSON document
  UPDATE users SET preferences = JSON_SET(preferences, '$.theme', 'dark') WHERE id = 5;
  ```

* **Validating JSON input:**

  ```sql
  -- Ensure that a string is a valid JSON document
  SELECT IS_JSON('{"name": "John", "age": 30}'); -- Returns 1
  ```

### Summary

MySQL's JSON functions allow for the creation, retrieval, manipulation, and modification of JSON data directly in SQL queries. These functions provide powerful tools to handle complex data structures like JSON objects and arrays, making it easier to store and process semi-structured data.
