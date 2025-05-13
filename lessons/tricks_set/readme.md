## 🔗 **Set Operation Tricks in SQL**

### ✴️ 1. **UNION vs UNION ALL**

```sql
-- Trick: Combine distinct rows from two queries
SELECT name FROM customers
UNION
SELECT name FROM leads;

-- Trick: Faster, keeps duplicates
SELECT name FROM customers
UNION ALL
SELECT name FROM leads;
```

**Use `UNION`** when you want unique results.
**Use `UNION ALL`** when you want all rows and **better performance**.

---

### 🚫 2. **INTERSECT – Find Common Rows**

```sql
-- Trick: Get emails in both users and subscribers
SELECT email FROM users
INTERSECT
SELECT email FROM subscribers;
```

**Use when**: You want only matching rows from both sets.
📌 **MySQL tip**: Use `INNER JOIN` instead (INTERSECT not supported).

---

### ➖ 3. **EXCEPT / MINUS – Find What’s Missing**

```sql
-- Trick (PostgreSQL, SQL Server): A - B
SELECT email FROM users
EXCEPT
SELECT email FROM unsubscribed;

-- Trick (Oracle): Use MINUS
SELECT email FROM users
MINUS
SELECT email FROM unsubscribed;
```

**Use when**: You want rows in A but **not** in B.

---

### ⚠️ 4. **Column Count & Type Must Match**

```sql
-- Trick: Make UNION work with mismatched columns
SELECT id, name FROM users
UNION
SELECT customer_id, full_name FROM customers;
```

✔ Columns must be **same count** and **compatible types**.
❗Use `CAST()` if needed to align data types.

---

### 🧱 5. **Wrap Complex Queries with () in Set Ops**

```sql
-- Trick: Use parentheses for clarity
(SELECT name FROM students WHERE grade > 90)
UNION
(SELECT name FROM alumni WHERE honors = TRUE);
```

**Use always**: Prevents syntax issues and helps formatting nested queries.

---

### 💡 6. **ORDER BY Goes at the End Only**

```sql
-- Trick: Sort after set op
(SELECT name FROM users)
UNION
(SELECT name FROM admins)
ORDER BY name;
```

**Don't** put `ORDER BY` inside individual queries — it **only applies to final result**.

---

### 🧮 7. **Use `UNION ALL` + Aggregation for Set Counting**

```sql
-- Trick: Count how many times each email appears
SELECT email, COUNT(*) FROM (
  SELECT email FROM users
  UNION ALL
  SELECT email FROM newsletter
) AS combined
GROUP BY email;
```

**Use when**: You want to know overlap frequency across sets.

---
