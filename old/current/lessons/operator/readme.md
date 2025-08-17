## **SQL Operators**

SQL operators are symbols or keywords used in SQL statements to perform operations on values in a database. They allow for manipulating and comparing data to retrieve specific information. SQL operators are broadly classified into the following categories:

1. **Logical Operators**
2. **Comparison Operators**
3. **Arithmetic Operators**
4. **Special Operators**

---

### **1. Logical Operators**

Logical operators are used to combine multiple conditions in a SQL query and return a Boolean result (`TRUE`, `FALSE`, or `UNKNOWN`).

#### **AND**
- **Description**: Combines two or more conditions and returns `TRUE` if all conditions are true.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE condition1 AND condition2;
  ```

#### **OR**
- **Description**: Combines two or more conditions and returns `TRUE` if at least one of the conditions is true.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE condition1 OR condition2;
  ```

#### **NOT**
- **Description**: Reverses the Boolean result of a condition. If the condition is `TRUE`, it returns `FALSE`, and if the condition is `FALSE`, it returns `TRUE`.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE NOT condition;
  ```

#### **Usage Examples**:
- **AND**: 
  ```sql
  SELECT * FROM employees WHERE salary > 50000 AND department = 'HR';
  ```
- **OR**: 
  ```sql
  SELECT * FROM products WHERE price < 100 OR category = 'Electronics';
  ```
- **NOT**: 
  ```sql
  SELECT * FROM employees WHERE NOT department = 'Sales';
  ```

---

### **2. Comparison Operators**

Comparison operators are used to compare two values or expressions. They return a Boolean result (`TRUE`, `FALSE`, or `UNKNOWN`).

#### **= (Equal to)**
- **Description**: Compares if two values are equal.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE column_name = value;
  ```

#### **!= (Not equal to)**
- **Description**: Compares if two values are not equal. This operator is supported by some databases like MySQL and PostgreSQL.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE column_name != value;
  ```

#### **<> (Not equal to)**
- **Description**: Another form of the "not equal to" operator, supported by most databases.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE column_name <> value;
  ```

#### **> (Greater than)**
- **Description**: Compares if the value is greater than the specified value.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE column_name > value;
  ```

#### **< (Less than)**
- **Description**: Compares if the value is less than the specified value.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE column_name < value;
  ```

#### **>= (Greater than or equal to)**
- **Description**: Compares if the value is greater than or equal to the specified value.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE column_name >= value;
  ```

#### **<= (Less than or equal to)**
- **Description**: Compares if the value is less than or equal to the specified value.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE column_name <= value;
  ```

#### **Usage Examples**:
- `=`
  ```sql
  SELECT * FROM employees WHERE department = 'HR';
  ```
- `!=` or `<>`
  ```sql
  SELECT * FROM employees WHERE department != 'HR';
  ```
- `>`
  ```sql
  SELECT * FROM products WHERE price > 100;
  ```
- `<=`
  ```sql
  SELECT * FROM products WHERE price <= 500;
  ```

---

### **3. Arithmetic Operators**

Arithmetic operators are used to perform mathematical calculations.

#### **+ (Addition)**
- **Description**: Adds two values.
- **Syntax**:
  ```sql
  SELECT column1 + column2
  FROM table_name;
  ```

#### **- (Subtraction)**
- **Description**: Subtracts one value from another.
- **Syntax**:
  ```sql
  SELECT column1 - column2
  FROM table_name;
  ```

#### **\* (Multiplication)**
- **Description**: Multiplies two values.
- **Syntax**:
  ```sql
  SELECT column1 * column2
  FROM table_name;
  ```

#### **/ (Division)**
- **Description**: Divides one value by another.
- **Syntax**:
  ```sql
  SELECT column1 / column2
  FROM table_name;
  ```

#### **Usage Examples**:
- `+`
  ```sql
  SELECT salary + bonus FROM employees;
  ```
- `-`
  ```sql
  SELECT price - discount FROM products;
  ```
- `*`
  ```sql
  SELECT quantity * price FROM order_details;
  ```
- `/`
  ```sql
  SELECT total_amount / quantity FROM order_details;
  ```

---

### **4. Special Operators**

Special operators provide more advanced functionality for filtering and working with data.

#### **LIKE**
- **Description**: Used to search for a specified pattern in a column. It supports wildcards:
  - `%`: Matches zero or more characters.
  - `_`: Matches a single character.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE column_name LIKE pattern;
  ```

#### **IN**
- **Description**: Used to check if a value matches any value in a list or subquery.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE column_name IN (value1, value2, value3);
  ```

#### **EXISTS**
- **Description**: Used to check if a subquery returns any result. If the subquery returns at least one row, `EXISTS` returns `TRUE`.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE EXISTS (SELECT 1 FROM another_table WHERE condition);
  ```

#### **ANY/ALL**
- **Description**:
  - **ANY**: Compares a value to any value in a list or result set. The condition is `TRUE` if it meets at least one condition.
  - **ALL**: Compares a value to all values in a list or result set. The condition is `TRUE` if it meets all conditions.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE column_name > ANY (SELECT column_name FROM another_table);
  ```

#### **BETWEEN**
- **Description**: Used to filter the result set within a certain range (inclusive). It can be used with numbers, text, or dates.
- **Syntax**:
  ```sql
  SELECT column_name
  FROM table_name
  WHERE column_name BETWEEN value1 AND value2;
  ```

#### **Usage Examples**:
- **LIKE**:
  ```sql
  SELECT * FROM employees WHERE name LIKE 'J%';
  ```
- **IN**:
  ```sql
  SELECT * FROM products WHERE category IN ('Electronics', 'Furniture');
  ```
- **EXISTS**:
  ```sql
  SELECT * FROM customers WHERE EXISTS (SELECT 1 FROM orders WHERE customer_id = customers.id);
  ```
- **ANY**:
  ```sql
  SELECT * FROM products WHERE price > ANY (SELECT price FROM products WHERE category = 'Electronics');
  ```
- **BETWEEN**:
  ```sql
  SELECT * FROM products WHERE price BETWEEN 100 AND 500;
  ```

---

### **Conclusion**

SQL operators form the foundation of query logic, enabling users to perform detailed and dynamic searches. By mastering logical, comparison, arithmetic, and special operators, you can create more complex and powerful queries to retrieve and manipulate data efficiently. These operators, when used strategically, help optimize data retrieval, improve query performance, and support a wide variety of use cases across databases.