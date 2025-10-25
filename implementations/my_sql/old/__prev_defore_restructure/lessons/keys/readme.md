## Keys in MySQL

In MySQL, **keys** are crucial for organizing and optimizing data within a database. They define relationships between tables and ensure the integrity and efficiency of data operations. MySQL supports various types of keys, such as **Primary Keys**, **Foreign Keys**, **Unique Keys**, and **Index Keys**, each serving different purposes in the database schema.

---

### Table of Contents

1. [Overview of Keys](#overview-of-keys)
2. [Primary Key](#primary-key)
3. [Foreign Key](#foreign-key)
4. [Unique Key](#unique-key)
5. [Index Key](#index-key)
6. [Full-Text Key](#full-text-key)
7. [Composite Key](#composite-key)
8. [Creating and Managing Keys](#creating-and-managing-keys)
9. [Best Practices](#best-practices)

---

### Overview of Keys

Keys in MySQL serve as constraints and indexes for improving data retrieval and ensuring **data integrity**. They play a critical role in maintaining the relationships between different tables, ensuring that the database operations (like `INSERT`, `UPDATE`, and `DELETE`) maintain consistency and correctness.

---

### Primary Key

A **Primary Key** is a field (or a combination of fields) that uniquely identifies each row in a table. A table can have only **one primary key**. The primary key must contain **unique values** and cannot contain **NULL** values.

* **Enforces Uniqueness**: Guarantees that the value of the primary key is unique for each record in the table.
* **Implicit Index**: Automatically creates a unique index for the primary key.

#### Syntax:

```sql
PRIMARY KEY (column_name)
```

**Example**:

```sql
CREATE TABLE employees (
  id INT PRIMARY KEY,   -- id is the Primary Key
  name VARCHAR(100),
  position VARCHAR(100)
);
```

---

### Foreign Key

A **Foreign Key** is a field (or a collection of fields) in one table that refers to the **Primary Key** of another table. It establishes a relationship between the two tables and ensures **referential integrity**. A foreign key can be **NULL** if the relationship is optional.

* **Maintains Referential Integrity**: Ensures that a foreign key value corresponds to a valid value in the referenced table.
* **Cascading Actions**: Supports actions like `ON DELETE CASCADE`, `ON UPDATE CASCADE`, etc., to define what happens when the referenced record is deleted or updated.

#### Syntax:

```sql
FOREIGN KEY (column_name) REFERENCES other_table(column_name)
```

**Example**:

```sql
CREATE TABLE orders (
  order_id INT PRIMARY KEY,
  customer_id INT,
  FOREIGN KEY (customer_id) REFERENCES customers(customer_id) ON DELETE CASCADE
);
```

---

### Unique Key

A **Unique Key** ensures that all values in a column (or a combination of columns) are unique across the table. Unlike a primary key, a table can have **multiple unique keys**, and they can accept **NULL** values (though only one NULL per unique key).

* **Enforces Uniqueness**: Ensures that no two rows have the same value for the specified column(s).
* **Allows NULL Values**: Unique keys can allow multiple `NULL` values.

#### Syntax:

```sql
UNIQUE (column_name)
```

**Example**:

```sql
CREATE TABLE users (
  user_id INT PRIMARY KEY,
  email VARCHAR(100) UNIQUE   -- email must be unique
);
```

---

### Index Key

An **Index Key** is used to improve the performance of queries that involve searching or sorting by specific columns. Indexes allow MySQL to find data faster, reducing the time required to process queries.

* **Improves Query Performance**: Speeds up `SELECT` queries, especially with `WHERE`, `ORDER BY`, and `JOIN` clauses.
* **Not Uniqueness-Enforcing**: Unlike primary and unique keys, index keys do not enforce uniqueness. They simply optimize data retrieval.

#### Syntax:

```sql
INDEX index_name (column_name)
```

**Example**:

```sql
CREATE TABLE products (
  product_id INT PRIMARY KEY,
  name VARCHAR(100),
  price DECIMAL(10, 2),
  INDEX price_index(price)  -- Index on the price column for faster queries
);
```

---

### Full-Text Key

A **Full-Text Key** is used to enable **full-text search** capabilities. It allows searching for keywords in text-based columns (e.g., `CHAR`, `TEXT`, `VARCHAR`) in a more efficient manner.

* **Full-Text Search**: Enables more advanced searches, such as searching for words or phrases within a text field, supporting boolean operators.
* **Requires Full-Text Index**: The column must have a **full-text index** before performing full-text search operations.

#### Syntax:

```sql
FULLTEXT (column_name)
```

**Example**:

```sql
CREATE TABLE articles (
  article_id INT PRIMARY KEY,
  title VARCHAR(255),
  content TEXT,
  FULLTEXT (title, content)  -- Full-text index on title and content columns
);
```

---

### Composite Key

A **Composite Key** is a primary key or unique key that is made up of multiple columns. It is used when a single column cannot uniquely identify a record, but a combination of columns can.

* **Multiple Columns**: Combines two or more columns to form a unique key.
* **Used for Many-to-Many Relationships**: Often used in **junction tables** for many-to-many relationships.

#### Syntax:

```sql
PRIMARY KEY (column1, column2, ...)
```

**Example**:

```sql
CREATE TABLE order_items (
  order_id INT,
  product_id INT,
  quantity INT,
  PRIMARY KEY (order_id, product_id)  -- Composite Primary Key
);
```

---

### Creating and Managing Keys

* **Creating Keys**: Keys are usually defined during table creation using the `CREATE TABLE` statement. They can also be added or modified later using `ALTER TABLE`.

#### Add a Primary Key After Table Creation:

```sql
ALTER TABLE employees
ADD PRIMARY KEY (id);
```

#### Add a Foreign Key After Table Creation:

```sql
ALTER TABLE orders
ADD CONSTRAINT fk_customer FOREIGN KEY (customer_id) REFERENCES customers(customer_id);
```

#### Add a Unique Key After Table Creation:

```sql
ALTER TABLE users
ADD UNIQUE (email);
```

#### Add an Index Key After Table Creation:

```sql
ALTER TABLE products
ADD INDEX (price);
```

---

### Best Practices

* **Primary Key**: Always define a primary key for every table. This key should be **NOT NULL** and **UNIQUE** to ensure that each record is identifiable.
* **Foreign Key**: Use foreign keys to maintain **referential integrity** between related tables. Ensure that foreign keys are indexed for faster lookups.
* **Indexing**: Create indexes for columns that are frequently queried or used in joins. Avoid over-indexing, as it can slow down `INSERT` and `UPDATE` operations.
* **Composite Key**: Use composite keys when a single column cannot uniquely identify a record, but a combination of columns can.
* **Full-Text Search**: Use full-text keys for advanced text search capabilities on large textual columns.
* **Normalization**: Normalize your tables to reduce redundancy, but ensure the use of foreign keys and indexes to maintain query performance.

---

### Summary

In MySQL, **keys** are fundamental components used to ensure **data integrity**, **optimize queries**, and define **relationships** between tables. The types of keys include **Primary Keys**, **Foreign Keys**, **Unique Keys**, **Index Keys**, **Full-Text Keys**, and **Composite Keys**, each serving distinct purposes to manage data efficiently. By carefully choosing the appropriate key for each use case, developers can ensure both data integrity and optimal performance.
