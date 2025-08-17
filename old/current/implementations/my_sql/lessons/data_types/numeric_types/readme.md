## Numeric Data Types in MySQL
 o
---

### Overview

Numeric data types in MySQL are used to store numerical values, both integers and floating-point numbers. These types determine how numbers are stored and their valid range. They are essential for handling calculations, counters, financial figures, and other number-based operations.

---

### Numeric Data Types

| Data Type   | Description                                     | Storage       | Range                                             | Example                                      |
|-------------|-------------------------------------------------|---------------|---------------------------------------------------|----------------------------------------------|
| **INT**     | Stores integers                                 | 4 bytes       | `-2147483648` to `2147483647` (signed)           | `CREATE TABLE users (user_id INT);`          |
| **BIGINT**  | Stores large integers                           | 8 bytes       | `-9223372036854775808` to `9223372036854775807`   | `CREATE TABLE transactions (transaction_id BIGINT);` |
| **FLOAT**   | Stores single-precision floating-point numbers  | 4 bytes       | Varies by precision                              | `CREATE TABLE products (price FLOAT);`       |
| **DOUBLE**  | Stores double-precision floating-point numbers  | 8 bytes       | Varies by precision                              | `CREATE TABLE measurements (length DOUBLE);`|
| **DECIMAL** | Stores exact decimal numbers                   | Varies        | Depends on precision and scale                   | `CREATE TABLE invoices (amount DECIMAL(10,2));` |

---

### Detailed Breakdown of Numeric Data Types

---

#### **INT**

- **Description**: Stores whole numbers without fractional components.
- **Storage**: 4 bytes.
- **Range**: 
  - **SIGNED**: `-2147483648` to `2147483647`
  - **UNSIGNED**: `0` to `4294967295`
- **Use Cases**: Common for storing identifiers (e.g., user IDs), counters, and small to medium-size integers.
- **Example**:  
  ```sql
  CREATE TABLE users (user_id INT);
  ```

---

#### **BIGINT**

- **Description**: Stores very large whole numbers, often used for larger integer values.
- **Storage**: 8 bytes.
- **Range**:
  - **SIGNED**: `-9223372036854775808` to `9223372036854775807`
  - **UNSIGNED**: `0` to `18446744073709551615`
- **Use Cases**: Typically used for large quantities, such as transaction IDs, large counters, or financial data where values exceed the range of INT.
- **Example**:  
  ```sql
  CREATE TABLE transactions (transaction_id BIGINT);
  ```

---

#### **FLOAT**

- **Description**: Stores single-precision floating-point numbers. Used for numbers with decimals, but with limited precision.
- **Storage**: 4 bytes.
- **Range**: Varies by the precision specified, but usually within ±3.4E+38 with 7 decimal digits of precision.
- **Use Cases**: Ideal for approximate values or measurements where the precision is not critical, such as storing prices or weights.
- **Example**:  
  ```sql
  CREATE TABLE products (price FLOAT);
  ```

---

#### **DOUBLE**

- **Description**: Stores double-precision floating-point numbers. More precise than FLOAT, typically used for scientific calculations.
- **Storage**: 8 bytes.
- **Range**: Varies by the precision, but usually within ±1.8E+308 with 15 decimal digits of precision.
- **Use Cases**: Used when higher precision is required, such as in financial data, scientific applications, and calculations involving large ranges.
- **Example**:  
  ```sql
  CREATE TABLE measurements (length DOUBLE);
  ```

---

#### **DECIMAL**

- **Description**: Stores exact decimal numbers, which makes it ideal for precise calculations (e.g., monetary values) without rounding errors.
- **Storage**: Varies depending on the precision and scale.
  - **Precision**: Total number of digits (both to the left and right of the decimal point).
  - **Scale**: Number of digits to the right of the decimal point.
- **Range**: Depends on the precision and scale defined.
- **Use Cases**: Primarily used for financial data or other applications where precision is essential, such as storing exact monetary values or quantities.
- **Example**:  
  ```sql
  CREATE TABLE invoices (amount DECIMAL(10,2));
  ```

---

### Choosing the Right Numeric Data Type

| Data Type   | Use Case                                           | Storage Type       |
|-------------|---------------------------------------------------|--------------------|
| **INT/BIGINT** | Whole numbers (IDs, counters)                    | Numeric (integer)  |
| **FLOAT/DOUBLE** | Floating-point numbers (prices, measurements)    | Numeric (float)    |
| **DECIMAL**  | Exact decimal numbers (financial data)            | Numeric (decimal)  |

---

### Summary

- **INT**: Suitable for small to medium-sized integers (e.g., IDs, counters).
- **BIGINT**: Used when dealing with large numbers that exceed the range of INT (e.g., large transactions, high-volume counters).
- **FLOAT/DOUBLE**: Ideal for storing floating-point numbers, with DOUBLE providing higher precision than FLOAT.
- **DECIMAL**: Best for cases where exact decimal representation is required, like financial data, to avoid rounding issues.

---
