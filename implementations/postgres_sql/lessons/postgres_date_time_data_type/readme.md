### PostgreSQL Date & Time Data Types  

#### Date & Time Types  
| Data Type          | Size  | Format | Notes |
|--------------------|------|----------------------|------------------------------------------------|
| `date`            | 4 bytes | YYYY-MM-DD | Stores only the date (year, month, day). |
| `time`            | 8 bytes | HH:MI:SS | Stores only the time of day. |
| `time with time zone` (`timetz`) | 12 bytes | HH:MI:SS±TZ | Stores time with a time zone offset. |
| `timestamp`       | 8 bytes | YYYY-MM-DD HH:MI:SS | Stores date and time without time zone. |
| `timestamp with time zone` (`timestamptz`) | 8 bytes | YYYY-MM-DD HH:MI:SS±TZ | Stores date and time with automatic UTC conversion. |
| `interval`        | 16 bytes | `1 year 2 months 3 days` | Stores a time span (duration). |

#### Key Differences  
| Feature | `date` | `time` | `timestamp` | `timestamptz` |
|---------|------|------|-----------|--------------|
| Stores Time | No | Yes | Yes | Yes |
| Stores Date | Yes | No | Yes | Yes |
| Time Zone Support | No | Yes | No | Yes |
| Use Case | Birthdays, events | Office hours | Logs, records | Global timestamps |

#### Interval Type  
Used to store a time span.  
- **Examples:**  
  ```sql
  '1 year 2 months'::interval
  '3 days 4 hours 30 minutes'::interval
  ```

#### Usage Scenarios  
| Scenario | Recommended Type |
|----------|----------------|
| Storing birthdates, deadlines | `date` |
| Storing opening/closing hours | `time` |
| Storing event timestamps | `timestamp` |
| Storing global timestamps (e.g., UTC-based logs) | `timestamptz` |
| Storing time duration (e.g., subscription length) | `interval` |

---