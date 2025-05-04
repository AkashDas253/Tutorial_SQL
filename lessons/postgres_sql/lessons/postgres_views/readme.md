### PostgreSQL Views  

#### **Overview**  
A **view** in PostgreSQL is a virtual table that represents the result of a query. It does not store data but provides a way to simplify complex queries, improve security, and enhance reusability.

---

### **1. Creating Views**  

- **Basic View**  
  ```sql
  CREATE VIEW employee_view AS
  SELECT id, name, department_id FROM employees;
  ```

- **View with Joins**  
  ```sql
  CREATE VIEW employee_department AS
  SELECT e.id, e.name, d.name AS department
  FROM employees e
  INNER JOIN departments d ON e.department_id = d.id;
  ```

- **View with Aggregation**  
  ```sql
  CREATE VIEW department_salary AS
  SELECT department_id, AVG(salary) AS avg_salary
  FROM employees
  GROUP BY department_id;
  ```

---

### **2. Querying Views**  

- **Selecting Data from a View**  
  ```sql
  SELECT * FROM employee_view;
  ```

- **Filtering Data in a View**  
  ```sql
  SELECT * FROM employee_department WHERE department = 'IT';
  ```

---

### **3. Updating Views**  

- **Modifying an Existing View**  
  ```sql
  CREATE OR REPLACE VIEW employee_view AS
  SELECT id, name, salary FROM employees;
  ```

- **Dropping a View**  
  ```sql
  DROP VIEW employee_view;
  ```

---

### **4. Updatable Views**  
- A view can be updatable if it meets certain conditions (e.g., no joins, no aggregation).  

**Example:**  
```sql
CREATE VIEW employee_basic AS
SELECT id, name, salary FROM employees;
```
```sql
UPDATE employee_basic SET salary = 60000 WHERE id = 1;
```

---

### **5. Materialized Views**  
- Stores data physically, unlike normal views.  
- Needs manual refresh when underlying data changes.

- **Creating a Materialized View**  
  ```sql
  CREATE MATERIALIZED VIEW sales_summary AS
  SELECT region, SUM(sales) AS total_sales
  FROM sales
  GROUP BY region;
  ```

- **Refreshing a Materialized View**  
  ```sql
  REFRESH MATERIALIZED VIEW sales_summary;
  ```

- **Dropping a Materialized View**  
  ```sql
  DROP MATERIALIZED VIEW sales_summary;
  ```

---

### **6. View Performance Considerations**  

| Factor | Impact |
|--------|--------|
| Normal views | Query executes every time the view is accessed. |
| Materialized views | Stores data, reducing query execution time. |
| Indexing | Improve performance on materialized views. |

---