## PL/SQL Collections

PL/SQL **collections** are data structures that can store multiple values of the same type. They are similar to arrays in other programming languages but offer more flexibility and functionality. Collections allow you to handle a set of data in a structured way, making it easier to work with groups of related items.

---

### **Types of PL/SQL Collections**

PL/SQL provides three types of collections:

| **Collection Type** | **Description**                                                      |
|---------------------|----------------------------------------------------------------------|
| **Associative Arrays (Index-by Tables)** | Collections with an **index** to access values. The index can be of any scalar type (e.g., `NUMBER`, `VARCHAR2`). |
| **Nested Tables**    | Similar to arrays but **dynamic** in size. They can be used like regular tables but can have **NULL** elements. |
| **Varrays (Variable-Size Arrays)** | Arrays with a **fixed size**, meaning they can only hold a predefined number of elements. |

---

### **Associative Arrays (Index-by Tables)**

Associative arrays store elements using an **index** (key). The index is **not restricted to consecutive integers** and can be any scalar type like `VARCHAR2`, `NUMBER`, etc.

#### **Declaration and Usage**

```plsql
DECLARE
  TYPE assoc_array IS TABLE OF VARCHAR2(50) INDEX BY VARCHAR2(20);
  emp_names assoc_array;
BEGIN
  emp_names('E001') := 'John';
  emp_names('E002') := 'Jane';
  
  DBMS_OUTPUT.PUT_LINE(emp_names('E001')); -- Output: John
END;
```

- **Associative arrays** are created using the `INDEX BY` keyword.
- The index type can be any **scalar data type**, such as `NUMBER` or `VARCHAR2`.
- Associative arrays are best used when you need to access elements using a **non-contiguous key**.

---

### **Nested Tables**

Nested tables are like regular tables, but they can **grow dynamically** and do not require a fixed size. They can store NULL values and do not have a limit on the number of elements they can hold, unlike varrays.

#### **Declaration and Usage**

```plsql
DECLARE
  TYPE num_table IS TABLE OF NUMBER;
  nums num_table := num_table(10, 20, 30, 40);
BEGIN
  FOR i IN 1..nums.COUNT LOOP
    DBMS_OUTPUT.PUT_LINE(nums(i)); -- Output: 10, 20, 30, 40
  END LOOP;
END;
```

- **Nested tables** are declared using `TYPE` and can be **initialized** with values.
- You can access elements using an **index** starting from 1.
- Nested tables are **dynamic** in size and can be stored in database columns of type `TABLE` or `VARRAY`.

---

### **Varrays (Variable-Size Arrays)**

Varrays are collections with a **fixed size** defined at the time of declaration. They are particularly useful when you need to limit the number of elements in a collection.

#### **Declaration and Usage**

```plsql
DECLARE
  TYPE varray_example IS VARRAY(5) OF VARCHAR2(50);  -- Max 5 elements
  cities varray_example := varray_example('New York', 'Los Angeles', 'Chicago');
BEGIN
  DBMS_OUTPUT.PUT_LINE(cities(1)); -- Output: New York
END;
```

- **Varrays** have a **maximum size** specified during their creation and are stored as a **single unit** in memory.
- Varrays can be useful when the number of elements is known ahead of time and limited in number.
- They are more efficient for **small collections** that don't grow dynamically.

---

### **Methods to Work with Collections**

PL/SQL collections support a variety of built-in methods that make it easy to manipulate data within them.

| **Method**      | **Description**                                                       |
|-----------------|-----------------------------------------------------------------------|
| `COUNT`         | Returns the number of elements in the collection.                     |
| `EXTEND`        | Adds elements to the collection (useful for nested tables and varrays). |
| `TRIM`          | Removes elements from the collection.                                 |
| `DELETE`        | Deletes all elements or a specific element in the collection.         |
| `FIRST`         | Returns the first element's index in the collection.                  |
| `LAST`          | Returns the last element's index in the collection.                   |
| `NEXT`          | Returns the index of the next element in the collection.              |
| `PRIOR`         | Returns the index of the previous element in the collection.          |

---

### **Collection Operations**

#### **COUNT Method**

The `COUNT` method is used to retrieve the number of elements in a collection.

```plsql
DECLARE
  TYPE emp_names IS TABLE OF VARCHAR2(50);
  names emp_names := emp_names('John', 'Jane', 'Smith');
BEGIN
  DBMS_OUTPUT.PUT_LINE('Number of employees: ' || names.COUNT); -- Output: 3
END;
```

#### **EXTEND Method**

The `EXTEND` method is used to add elements to a collection.

```plsql
DECLARE
  TYPE num_table IS TABLE OF NUMBER;
  nums num_table := num_table(10, 20);
BEGIN
  nums.EXTEND(2); -- Extends the collection by 2 elements
  nums(3) := 30;
  nums(4) := 40;
  
  FOR i IN 1..nums.COUNT LOOP
    DBMS_OUTPUT.PUT_LINE(nums(i)); -- Output: 10, 20, 30, 40
  END LOOP;
END;
```

#### **TRIM Method**

The `TRIM` method removes elements from the collection.

```plsql
DECLARE
  TYPE num_table IS TABLE OF NUMBER;
  nums num_table := num_table(10, 20, 30, 40);
BEGIN
  nums.TRIM(2); -- Removes 2 elements from the end
  FOR i IN 1..nums.COUNT LOOP
    DBMS_OUTPUT.PUT_LINE(nums(i)); -- Output: 10, 20
  END LOOP;
END;
```

#### **DELETE Method**

The `DELETE` method can remove elements from a collection. It can either delete a specific element or clear the entire collection.

```plsql
DECLARE
  TYPE num_table IS TABLE OF NUMBER;
  nums num_table := num_table(10, 20, 30, 40);
BEGIN
  nums.DELETE; -- Deletes all elements from the collection
  DBMS_OUTPUT.PUT_LINE('Number of elements after delete: ' || nums.COUNT); -- Output: 0
END;
```

---

### **Using Collections in SQL Queries**

PL/SQL collections can be used to store data in variables, and then these collections can be passed to SQL queries. They are especially useful when working with bulk operations.

#### **Example: Using Nested Tables in SQL**

```plsql
DECLARE
  TYPE num_table IS TABLE OF NUMBER;
  nums num_table := num_table(10, 20, 30);
BEGIN
  FOR i IN 1..nums.COUNT LOOP
    INSERT INTO numbers_table (num_column) VALUES (nums(i)); -- Bulk insert into table
  END LOOP;
  COMMIT;
END;
```

In this example, a nested table is used to insert multiple rows into a database table in a loop.

---

### **Summary**

PL/SQL collections are powerful tools for handling multiple values efficiently. They come in three primary types:
- **Associative arrays** (Index-by tables) allow you to access elements by non-contiguous indices.
- **Nested tables** are dynamic in size and do not require fixed lengths.
- **Varrays** are fixed-size collections with a predefined number of elements.

PL/SQL provides various methods such as `COUNT`, `EXTEND`, `TRIM`, and `DELETE` to manipulate these collections. They are essential for **bulk operations** and **dynamic data handling**, and they can be used in conjunction with SQL queries for efficient database interaction.
