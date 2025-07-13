## **PostgreSQL Date & Time Data Types, Functions, and Operations**  

---

### **1. Date & Time Data Types**  
| Data Type | Storage | Format | Notes |
|-----------|--------|--------|-------|
| `DATE` | 4 bytes | `YYYY-MM-DD` | Stores only date |
| `TIME` | 8 bytes | `HH:MI:SS` | Stores only time |
| `TIME WITH TIME ZONE` (`TIMETZ`) | 12 bytes | `HH:MI:SS+TZ` | Stores time with time zone |
| `TIMESTAMP` | 8 bytes | `YYYY-MM-DD HH:MI:SS` | Stores date & time |
| `TIMESTAMP WITH TIME ZONE` (`TIMESTAMPTZ`) | 12 bytes | `YYYY-MM-DD HH:MI:SS+TZ` | Stores date & time with time zone |
| `INTERVAL` | 16 bytes | `days hours:minutes:seconds` | Stores time intervals |

---

### **2. Current Date & Time Functions**  
| Function | Description | Example Output |
|----------|-------------|---------------|
| `CURRENT_DATE` | Returns current date | `2025-02-21` |
| `CURRENT_TIME` | Returns current time | `14:30:45.123456` |
| `CURRENT_TIMESTAMP` | Returns current date & time | `2025-02-21 14:30:45.123456` |
| `NOW()` | Returns current timestamp | `2025-02-21 14:30:45.123456` |
| `TIMEOFDAY()` | Returns textual representation of current time | `Fri Feb 21 14:30:45 2025` |
| `CLOCK_TIMESTAMP()` | Returns actual current time (without transaction time freeze) | `2025-02-21 14:30:45.123456` |

---

### **3. Extracting & Formatting Date/Time**  
| Function | Description | Example | Output |
|----------|-------------|---------|--------|
| `EXTRACT(field FROM source)` | Extracts parts of date/time | `EXTRACT(YEAR FROM TIMESTAMP '2025-02-21 14:30:45')` | `2025` |
| `DATE_PART(field, source)` | Extracts parts of date/time | `DATE_PART('month', TIMESTAMP '2025-02-21 14:30:45')` | `2` |
| `TO_CHAR(value, format)` | Formats date/time as string | `TO_CHAR(NOW(), 'YYYY-MM-DD HH24:MI:SS')` | `'2025-02-21 14:30:45'` |

**Common Format Patterns:**
| Pattern | Description | Example Output |
|---------|-------------|---------------|
| `YYYY` | Year (4 digits) | `2025` |
| `YY` | Year (2 digits) | `25` |
| `MM` | Month (2 digits) | `02` |
| `Mon` | Abbreviated month | `Feb` |
| `Month` | Full month name | `February` |
| `DD` | Day of the month | `21` |
| `DY` | Abbreviated weekday | `Fri` |
| `Day` | Full weekday name | `Friday` |
| `HH24` | 24-hour format hour | `14` |
| `HH12` | 12-hour format hour | `02` |
| `MI` | Minutes | `30` |
| `SS` | Seconds | `45` |
| `AM/PM` | AM or PM | `PM` |

---

### **4. Date & Time Arithmetic**  
| Operation | Example | Output |
|-----------|---------|--------|
| Add Interval | `SELECT NOW() + INTERVAL '1 day';` | Adds 1 day |
| Subtract Interval | `SELECT NOW() - INTERVAL '2 hours';` | Subtracts 2 hours |
| Difference (days) | `SELECT AGE('2025-02-21', '2024-02-21');` | `1 year` |
| Difference (interval) | `SELECT '2025-02-21'::DATE - '2024-02-21'::DATE;` | `365` |

---

### **5. Interval Manipulation**  
| Function | Example | Output |
|----------|---------|--------|
| `JUSTIFY_DAYS(interval)` | `JUSTIFY_DAYS('30 days')` | `1 month` |
| `JUSTIFY_HOURS(interval)` | `JUSTIFY_HOURS('25 hours')` | `1 day 1 hour` |
| `JUSTIFY_INTERVAL(interval)` | `JUSTIFY_INTERVAL('60 days 25 hours')` | `2 months 1 day 1 hour` |
