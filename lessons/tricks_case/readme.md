## 🧑‍⚖️ **CASE Statements Tricks in SQL**

### 1. **Simple CASE Statement**

```sql
-- Trick: Use CASE for simple condition checking
SELECT name, salary, 
       CASE 
           WHEN salary > 50000 THEN 'High'
           WHEN salary > 30000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_level
FROM employees;
```

**Use when**: You need to evaluate simple conditions and categorize or transform data based on them.

---

### 2. **Searched CASE Statement (Multiple Conditions)**

```sql
-- Trick: Use multiple conditions with searched CASE for complex logic
SELECT name, salary, 
       CASE 
           WHEN salary > 70000 THEN 'Very High'
           WHEN salary BETWEEN 50000 AND 70000 THEN 'High'
           WHEN salary BETWEEN 30000 AND 50000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_level
FROM employees;
```

**Use when**: You need to evaluate multiple conditions, not just simple equality.

---

### 3. **CASE with Aggregates**

```sql
-- Trick: Apply CASE inside aggregate functions
SELECT department, 
       COUNT(CASE WHEN salary > 50000 THEN 1 END) AS high_salary_count,
       COUNT(CASE WHEN salary <= 50000 THEN 1 END) AS low_salary_count
FROM employees
GROUP BY department;
```

**Use when**: You want to apply conditional logic inside aggregate functions (like COUNT, SUM, etc.) for grouping.

---

### 4. **CASE in WHERE Clause**

```sql
-- Trick: Use CASE inside WHERE clause for conditional filtering
SELECT name, salary 
FROM employees
WHERE CASE 
            WHEN department = 'Sales' THEN salary > 40000
            WHEN department = 'HR' THEN salary > 30000
            ELSE salary > 25000
        END;
```

**Use when**: You need conditional filtering with complex logic in the `WHERE` clause.

---

### 5. **CASE in ORDER BY Clause**

```sql
-- Trick: Use CASE inside ORDER BY to dynamically sort based on conditions
SELECT name, salary, department
FROM employees
ORDER BY 
       CASE 
           WHEN department = 'Sales' THEN salary DESC
           ELSE salary ASC
       END;
```

**Use when**: You want to dynamically change the sorting behavior based on specific conditions.

---

### 6. **CASE with Multiple Else Conditions**

```sql
-- Trick: Use multiple ELSE conditions to handle several outcomes
SELECT name, salary, 
       CASE 
           WHEN department = 'Sales' THEN 'Sales Team'
           WHEN department = 'HR' THEN 'HR Team'
           ELSE 'Other'
       END AS department_category
FROM employees;
```

**Use when**: You need to map multiple conditions to distinct outcomes with several `WHEN` clauses.

---

### 7. **Nested CASE Statements**

```sql
-- Trick: Use CASE inside another CASE for multi-level conditional logic
SELECT name, salary, 
       CASE 
           WHEN salary > 70000 THEN 
               CASE 
                   WHEN department = 'Sales' THEN 'Sales High Earner'
                   ELSE 'Other High Earner'
               END
           ELSE 'Low Earner'
       END AS salary_category
FROM employees;
```

**Use when**: You need more complex logic with multiple layers of conditions inside `CASE`.

---

### 8. **CASE with NULL Handling**

```sql
-- Trick: Use CASE to replace NULL values with a default value
SELECT name, 
       CASE 
           WHEN salary IS NULL THEN 'No Salary Data'
           ELSE salary
       END AS salary_info
FROM employees;
```

**Use when**: You want to replace `NULL` values with a default or custom value.

---

### 9. **CASE in UPDATE Statement**

```sql
-- Trick: Use CASE in UPDATE statement for conditional updates
UPDATE employees
SET salary = CASE 
                 WHEN department = 'Sales' THEN salary * 1.1
                 WHEN department = 'HR' THEN salary * 1.05
                 ELSE salary * 1.02
             END
WHERE department IN ('Sales', 'HR');
```

**Use when**: You need to apply conditional logic while updating records based on specific criteria.

---

### 10. **CASE for Data Transformation**

```sql
-- Trick: Use CASE for data transformation (convert data format)
SELECT order_id, 
       CASE 
           WHEN order_status = 'P' THEN 'Pending'
           WHEN order_status = 'C' THEN 'Completed'
           ELSE 'Cancelled'
       END AS status_description
FROM orders;
```

**Use when**: You need to transform data values into more readable or categorized forms.

---

### 11. **CASE for Complex Data Mapping**

```sql
-- Trick: Use CASE to map one value to multiple outcomes
SELECT order_id, 
       CASE 
           WHEN payment_status = 'Paid' THEN 'Payment Received'
           WHEN payment_status = 'Pending' THEN 'Waiting for Payment'
           ELSE 'Payment Failed'
       END AS payment_status_message
FROM orders;
```

**Use when**: You need to perform complex mapping or categorization based on one or more conditions.

---

### 12. **CASE for Conditional Aggregation**

```sql
-- Trick: Apply conditional aggregation based on CASE
SELECT department, 
       SUM(CASE WHEN salary > 50000 THEN salary ELSE 0 END) AS high_salary_sum
FROM employees
GROUP BY department;
```

**Use when**: You want to conditionally aggregate values (like summing only salaries greater than 50k).

---

### 13. **CASE with Multiple Expressions**

```sql
-- Trick: Use multiple CASE statements to handle different logic
SELECT name, 
       CASE 
           WHEN salary > 70000 THEN 'High Salary'
           ELSE 'Low Salary'
       END AS salary_category,
       CASE 
           WHEN department = 'Sales' THEN 'Sales Team'
           ELSE 'Other Team'
       END AS team_type
FROM employees;
```

**Use when**: You need multiple conditional transformations or categorizations in the same query.

---

### 14. **CASE in SELECT with Expressions**

```sql
-- Trick: Use CASE for more complex data manipulations
SELECT name, salary,
       CASE 
           WHEN salary > 50000 THEN salary * 0.1
           ELSE salary * 0.05
       END AS bonus
FROM employees;
```

**Use when**: You need to apply a transformation based on a condition in the `SELECT` clause, like calculating bonuses.

---
