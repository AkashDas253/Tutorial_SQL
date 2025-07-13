## Control Structures in PL/SQL  

Control structures in PL/SQL allow you to define the flow of execution based on specific conditions or loops. These include conditional statements, loop structures, and more. These structures help manage the logic of your programs and enhance their flexibility.

---

### **Conditional Control Structures**

Conditional structures are used to execute different blocks of code based on certain conditions.

#### **IF-THEN Statement**

| **Syntax**                                           | **Description**                                         | **Example**                                                       |
|------------------------------------------------------|---------------------------------------------------------|-------------------------------------------------------------------|
| `IF condition THEN`<br> `statements;`<br> `END IF;`   | Executes the statements if the condition is true.       | ```IF v_salary > 5000 THEN<br> DBMS_OUTPUT.PUT_LINE('High'); END IF;``` |

#### **IF-THEN-ELSE Statement**

| **Syntax**                                           | **Description**                                         | **Example**                                                       |
|------------------------------------------------------|---------------------------------------------------------|-------------------------------------------------------------------|
| `IF condition THEN`<br> `statements;`<br> `ELSE`<br> `else_statements;`<br> `END IF;` | Executes the first set of statements if the condition is true, otherwise executes the else block. | ```IF v_salary > 5000 THEN<br> DBMS_OUTPUT.PUT_LINE('High');<br> ELSE<br> DBMS_OUTPUT.PUT_LINE('Low');<br> END IF;``` |

#### **IF-THEN-ELSIF-ELSE Statement**

| **Syntax**                                           | **Description**                                         | **Example**                                                       |
|------------------------------------------------------|---------------------------------------------------------|-------------------------------------------------------------------|
| `IF condition1 THEN`<br> `statements1;`<br> `ELSIF condition2 THEN`<br> `statements2;`<br> `ELSE`<br> `statements3;`<br> `END IF;` | Checks multiple conditions sequentially. If the first condition fails, it checks the next condition and so on. | ```IF v_salary > 5000 THEN<br> DBMS_OUTPUT.PUT_LINE('High');<br> ELSIF v_salary = 5000 THEN<br> DBMS_OUTPUT.PUT_LINE('Medium');<br> ELSE<br> DBMS_OUTPUT.PUT_LINE('Low');<br> END IF;``` |

---

### **Looping Control Structures**

PL/SQL provides various looping constructs to repeatedly execute code based on specific conditions.

#### **Basic LOOP**

| **Syntax**                                           | **Description**                                         | **Example**                                                       |
|------------------------------------------------------|---------------------------------------------------------|-------------------------------------------------------------------|
| `LOOP`<br> `statements;`<br> `EXIT WHEN condition;`<br> `END LOOP;` | Repeats statements until the specified condition is true. | ```LOOP<br> DBMS_OUTPUT.PUT_LINE('Running loop');<br> EXIT WHEN counter > 10;<br> END LOOP;``` |

#### **FOR LOOP**

| **Syntax**                                           | **Description**                                         | **Example**                                                       |
|------------------------------------------------------|---------------------------------------------------------|-------------------------------------------------------------------|
| `FOR counter IN start_value..end_value LOOP`<br> `statements;`<br> `END LOOP;` | Iterates through a range of values from start_value to end_value. | ```FOR i IN 1..5 LOOP<br> DBMS_OUTPUT.PUT_LINE('Value: ' || i);<br> END LOOP;``` |

#### **WHILE LOOP**

| **Syntax**                                           | **Description**                                         | **Example**                                                       |
|------------------------------------------------------|---------------------------------------------------------|-------------------------------------------------------------------|
| `WHILE condition LOOP`<br> `statements;`<br> `END LOOP;` | Continues executing the loop as long as the condition is true. | ```WHILE counter <= 10 LOOP<br> DBMS_OUTPUT.PUT_LINE(counter);<br> counter := counter + 1;<br> END LOOP;``` |

---

### **EXIT Statement**

The `EXIT` statement is used to exit from a loop or block based on a specified condition.

| **Syntax**                                | **Description**                                      | **Example**                                                           |
|-------------------------------------------|------------------------------------------------------|-----------------------------------------------------------------------|
| `EXIT WHEN condition;`                    | Exits from the loop if the condition is true.        | ```LOOP<br> EXIT WHEN counter = 5;<br> END LOOP;```                   |
| `EXIT;`                                    | Exits from the nearest enclosing loop immediately.   | ```FOR i IN 1..10 LOOP<br> EXIT;<br> END LOOP;```                     |

---

### **CONTINUE Statement**

The `CONTINUE` statement is used to skip the remaining statements in the loop and proceed to the next iteration.

| **Syntax**                                | **Description**                                      | **Example**                                                           |
|-------------------------------------------|------------------------------------------------------|-----------------------------------------------------------------------|
| `CONTINUE;`                                | Skips to the next iteration of the loop.             | ```FOR i IN 1..5 LOOP<br> IF i = 3 THEN CONTINUE; END IF;<br> END LOOP;``` |

---

### **CASE Statement**

The `CASE` statement allows you to perform multiple conditional checks and execute different blocks based on the result.

#### **Simple CASE Statement**

| **Syntax**                                           | **Description**                                         | **Example**                                                       |
|------------------------------------------------------|---------------------------------------------------------|-------------------------------------------------------------------|
| `CASE expression`<br> `WHEN value1 THEN`<br> `statements1;`<br> `WHEN value2 THEN`<br> `statements2;`<br> `ELSE`<br> `else_statements;`<br> `END CASE;` | Compares the value of an expression with several possible values. | ```CASE v_salary<br> WHEN 5000 THEN<br> DBMS_OUTPUT.PUT_LINE('Medium');<br> WHEN 6000 THEN<br> DBMS_OUTPUT.PUT_LINE('High');<br> ELSE<br> DBMS_OUTPUT.PUT_LINE('Low');<br> END CASE;``` |

#### **Search CASE Statement**

| **Syntax**                                           | **Description**                                         | **Example**                                                       |
|------------------------------------------------------|---------------------------------------------------------|-------------------------------------------------------------------|
| `CASE`<br> `WHEN condition1 THEN`<br> `statements1;`<br> `WHEN condition2 THEN`<br> `statements2;`<br> `ELSE`<br> `else_statements;`<br> `END CASE;` | Compares multiple conditions to choose which block to execute. | ```CASE<br> WHEN v_salary > 5000 THEN<br> DBMS_OUTPUT.PUT_LINE('High');<br> WHEN v_salary = 5000 THEN<br> DBMS_OUTPUT.PUT_LINE('Medium');<br> ELSE<br> DBMS_OUTPUT.PUT_LINE('Low');<br> END CASE;``` |

---

### Summary of Control Structures

| **Control Structure** | **Description**                                          | **Example**                              |
|-----------------------|----------------------------------------------------------|------------------------------------------|
| **IF-THEN**           | Executes statements if the condition is true.            | `IF v_salary > 5000 THEN DBMS_OUTPUT.PUT_LINE('High'); END IF;` |
| **IF-THEN-ELSE**      | Executes one block if true, another if false.            | `IF v_salary > 5000 THEN DBMS_OUTPUT.PUT_LINE('High'); ELSE DBMS_OUTPUT.PUT_LINE('Low'); END IF;` |
| **IF-THEN-ELSIF-ELSE**| Checks multiple conditions sequentially.                 | `IF v_salary > 5000 THEN DBMS_OUTPUT.PUT_LINE('High'); ELSIF v_salary = 5000 THEN DBMS_OUTPUT.PUT_LINE('Medium'); ELSE DBMS_OUTPUT.PUT_LINE('Low'); END IF;` |
| **LOOP**              | Repeats statements until a condition is met.             | `LOOP DBMS_OUTPUT.PUT_LINE('Running loop'); EXIT WHEN counter > 10; END LOOP;` |
| **FOR LOOP**          | Iterates through a specified range of values.            | `FOR i IN 1..5 LOOP DBMS_OUTPUT.PUT_LINE(i); END LOOP;` |
| **WHILE LOOP**        | Repeats as long as the condition is true.                | `WHILE counter <= 10 LOOP DBMS_OUTPUT.PUT_LINE(counter); counter := counter + 1; END LOOP;` |
| **EXIT**              | Exits the loop when a condition is true.                 | `EXIT WHEN counter = 5;`                |
| **CONTINUE**          | Skips to the next iteration of a loop.                   | `CONTINUE;`                             |
| **CASE**              | Executes different blocks based on multiple conditions.  | `CASE WHEN v_salary > 5000 THEN DBMS_OUTPUT.PUT_LINE('High'); ELSE DBMS_OUTPUT.PUT_LINE('Low'); END CASE;` |

---