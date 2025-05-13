## 📊 **Aggregation Tricks in SQL**

### 🧠 1. **Basic Aggregates**

```sql
-- Trick: Get total, average, and count in one go
SELECT COUNT(*) AS total_users,
       AVG(age) AS avg_age,
       MAX(age) AS oldest,
       MIN(age) AS youngest
FROM users;
```

**Use when**: You want quick summary stats.

---

### 🎯 2. **Group By Multiple Columns**

```sql
-- Trick: Group sales by region and year
SELECT region, YEAR(sale_date) AS year, SUM(amount) AS total
FROM sales
GROUP BY region, YEAR(sale_date);
```

**Use when**: You need breakdowns by more than one attribute.

---

### ⚙️ 3. **Filter Aggregated Results with HAVING**

```sql
-- Trick: Find customers with >5 orders
SELECT customer_id, COUNT(*) AS orders
FROM orders
GROUP BY customer_id
HAVING COUNT(*) > 5;
```

**Use `HAVING`**: To filter **after aggregation** (not `WHERE`).

---

### ⚡ 4. **Aggregate + JOIN = Real Insights**

```sql
-- Trick: Total orders per user with names
SELECT u.name, COUNT(o.id) AS total_orders
FROM users u
JOIN orders o ON u.id = o.user_id
GROUP BY u.name;
```

**Use when**: You need aggregation with related info.

---

### 🧮 5. **Use CASE for Conditional Aggregates**

```sql
-- Trick: Count active/inactive users
SELECT 
  COUNT(CASE WHEN status = 'active' THEN 1 END) AS active,
  COUNT(CASE WHEN status = 'inactive' THEN 1 END) AS inactive
FROM users;
```

**Use when**: You want multiple metrics from one pass.

---

### 🧩 6. **GROUP BY ROLLUP**

```sql
-- Trick: Add subtotals and grand total
SELECT department, SUM(salary) 
FROM employees
GROUP BY ROLLUP(department);
```

**Use when**: You want subtotal and overall total **in one query**.

---

### 🔄 7. **GROUPING SETS for Custom Grouping**

```sql
-- Trick: Flexible grouping
SELECT department, role, SUM(salary)
FROM employees
GROUP BY GROUPING SETS (
  (department, role),
  (department),
  ()
);
```

**Use when**: You want multiple levels of aggregation at once.

---

### 🧭 8. **Aggregate Over All Rows (No GROUP BY)**

```sql
-- Trick: Average order value
SELECT SUM(amount)/COUNT(DISTINCT user_id) AS avg_order_value FROM orders;
```

**Use when**: You want overall stats, not grouped.

---

### 🧲 9. **Count Unique with COUNT(DISTINCT ...)**

```sql
-- Trick: Unique visitors
SELECT COUNT(DISTINCT user_id) AS unique_users FROM visits;
```

**Use when**: You need unique counts.

---

### 💡 10. **Use Aggregates in CTEs**

```sql
-- Trick: Use CTE for modular aggregates
WITH totals AS (
  SELECT user_id, COUNT(*) AS order_count FROM orders GROUP BY user_id
)
SELECT u.name, t.order_count
FROM users u JOIN totals t ON u.id = t.user_id;
```

**Use when**: You want clean, reusable aggregations.

---
