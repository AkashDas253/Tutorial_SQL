## 🔍 **Subquery Tricks in SQL**

### 1. **Basic Subquery in WHERE Clause**

```sql
-- Trick: Find users who made purchases in 2023
SELECT name FROM users
WHERE id IN (
  SELECT user_id FROM orders WHERE YEAR(order_date) = 2023
);
```

**Use when**: You need to filter based on results from another query.

---

### 2. **Subquery in SELECT Clause**

```sql
-- Trick: Get total spend per user
SELECT name,
       (SELECT SUM(amount) FROM orders WHERE user_id = u.id) AS total_spent
FROM users u;
```

**Use when**: You want to return additional calculated data in the main query.

---

### 3. **Correlated Subquery**

```sql
-- Trick: Find users who spent more than the average user
SELECT name FROM users u
WHERE (SELECT SUM(amount) FROM orders o WHERE o.user_id = u.id) > 
      (SELECT AVG(amount) FROM orders);
```

**Use when**: You need a subquery that references the outer query. (This is correlated.)

---

### 4. **Subquery in FROM Clause (Inline Views)**

```sql
-- Trick: Get the most recent order per user
SELECT user_id, MAX(order_date) AS last_order_date
FROM (
  SELECT user_id, order_date FROM orders ORDER BY order_date DESC
) AS recent_orders
GROUP BY user_id;
```

**Use when**: You want to perform operations on the result set of a subquery.

---

### 5. **Subquery with EXISTS**

```sql
-- Trick: Users who have placed an order
SELECT name FROM users u
WHERE EXISTS (
  SELECT 1 FROM orders o WHERE o.user_id = u.id
);
```

**Use when**: You only care about existence, not the actual values. **EXISTS** is usually more efficient than `IN` for large datasets.

---

### 6. **Subquery with NOT EXISTS**

```sql
-- Trick: Users who have not placed any orders
SELECT name FROM users u
WHERE NOT EXISTS (
  SELECT 1 FROM orders o WHERE o.user_id = u.id
);
```

**Use when**: You want to filter out users who don’t meet specific criteria (opposite of `EXISTS`).

---

### 7. **IN vs. EXISTS**

```sql
-- Trick: Use EXISTS for correlated queries
SELECT name FROM users u
WHERE EXISTS (
  SELECT 1 FROM orders o WHERE o.user_id = u.id AND o.amount > 100
);

-- Trick: Use IN for non-correlated subqueries
SELECT name FROM users
WHERE id IN (
  SELECT user_id FROM orders WHERE amount > 100
);
```

**Use `IN`** for non-correlated subqueries,
**Use `EXISTS`** when checking for the presence of a condition.

---

### 8. **Subquery with JOIN Alternative**

```sql
-- Trick: Same result with JOIN
SELECT u.name, o.amount
FROM users u
JOIN orders o ON u.id = o.user_id
WHERE o.amount > 100;
```

**Use when**: You can rewrite subqueries as joins for improved performance and simplicity.

---

### 9. **Subqueries in UPDATE Statements**

```sql
-- Trick: Update user status based on total orders
UPDATE users
SET status = 'VIP'
WHERE id IN (
  SELECT user_id FROM orders GROUP BY user_id HAVING COUNT(*) > 10
);
```

**Use when**: You need to update a table based on aggregate data or another query's result.

---

### 10. **Using Subqueries in DELETE Statements**

```sql
-- Trick: Delete users who have never placed an order
DELETE FROM users
WHERE id NOT IN (
  SELECT user_id FROM orders
);
```

**Use when**: You want to delete records based on conditions from a related table.

---

### 11. **Subqueries with Aggregates**

```sql
-- Trick: Find the users who spent more than the average spend
SELECT name FROM users u
WHERE (SELECT SUM(amount) FROM orders o WHERE o.user_id = u.id) > 
      (SELECT AVG(amount) FROM orders);
```

**Use when**: You need aggregate values within the subquery.

---
