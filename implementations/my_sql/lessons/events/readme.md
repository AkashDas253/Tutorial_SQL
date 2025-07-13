## Events

MySQL **Events** are scheduled database tasks that run automatically at specified times or intervals. They are like *cron jobs* for databases and are part of the **Event Scheduler**.

---

### Purpose

* Automate repetitive tasks (e.g., cleanup, summaries, reports).
* Schedule future data operations.
* Replace external cron jobs for DB logic.

---

### Event Scheduler

To use events, the **event scheduler must be enabled**:

```sql
SET GLOBAL event_scheduler = ON;
```

Check status:

```sql
SHOW VARIABLES LIKE 'event_scheduler';
```

---

### Syntax

```sql
CREATE EVENT [IF NOT EXISTS] event_name
ON SCHEDULE schedule
[ON COMPLETION [NOT] PRESERVE]
[ENABLE | DISABLE]
DO
event_body;
```

---

### Schedule Options

| Type                 | Syntax Example                                         | Description                        |
| -------------------- | ------------------------------------------------------ | ---------------------------------- |
| One-time             | `ON SCHEDULE AT '2025-06-01 00:00:00'`                 | Runs once at specified time        |
| Recurring (Interval) | `ON SCHEDULE EVERY 1 DAY STARTS '2025-06-01 00:00:00'` | Runs periodically starting at time |
| End Time             | `ENDS '2025-12-01 00:00:00'`                           | Optional: sets expiration time     |

---

### Example: Auto-archive Old Orders

```sql
CREATE EVENT archive_old_orders
ON SCHEDULE EVERY 1 DAY
STARTS CURRENT_TIMESTAMP
DO
  DELETE FROM orders WHERE order_date < NOW() - INTERVAL 90 DAY;
```

---

### Example: One-Time Data Update

```sql
CREATE EVENT update_prices_once
ON SCHEDULE AT '2025-06-01 10:00:00'
DO
  UPDATE products SET price = price * 1.05;
```

---

### Managing Events

| Operation            | Command                              |
| -------------------- | ------------------------------------ |
| Show all events      | `SHOW EVENTS [FROM db_name];`        |
| Show event details   | `SHOW CREATE EVENT event_name;`      |
| Alter an event       | `ALTER EVENT event_name ...;`        |
| Enable/disable event | `ALTER EVENT event_name ENABLE;`     |
| Drop event           | `DROP EVENT [IF EXISTS] event_name;` |

---

### Options

* `ON COMPLETION [NOT] PRESERVE`

  * `NOT PRESERVE`: event is dropped after it runs (default for one-time).
  * `PRESERVE`: event remains after execution (default for recurring).

* `ENABLE` / `DISABLE`
  Controls whether the event is active immediately.

---

### Use Cases

* **Automated Cleanup**: Remove old records regularly.
* **Data Archiving**: Move inactive data to archive tables.
* **Scheduled Updates**: Adjust prices or stats periodically.
* **Reporting Tasks**: Generate or refresh summary tables.

---

### Notes

* Event bodies can contain any valid SQL (except user interaction).
* Time is based on `EVENT_TIME_ZONE`, default is `SYSTEM`.
* Requires **EVENT privilege** to create/drop events.

---
