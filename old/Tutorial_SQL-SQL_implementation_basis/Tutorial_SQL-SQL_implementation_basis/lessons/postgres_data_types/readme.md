## **PostgreSQL Data Types Cheatsheet**  

#### **1. Numeric Types**  
| Type                   | Storage | Range / Precision | Use Case | Example |
|------------------------|---------|------------------|----------|---------|
| `smallint`            | 2 bytes | -32,768 to 32,767 | Small counters, status codes | `CREATE TABLE users (id SMALLINT PRIMARY KEY);` |
| `integer`             | 4 bytes | -2^31 to 2^31-1 | General-purpose numeric data | `CREATE TABLE products (price INTEGER NOT NULL);` |
| `bigint`              | 8 bytes | -2^63 to 2^63-1 | Large numbers (e.g., user IDs, financial data) | `CREATE TABLE transactions (amount BIGINT);` |
| `decimal(p,s)` / `numeric(p,s)` | Variable | Exact precision | Financial calculations | `CREATE TABLE payments (amount DECIMAL(10,2));` |
| `real`               | 4 bytes | 6 decimal digits precision | Scientific computations | `CREATE TABLE sensors (temperature REAL);` |
| `double precision`   | 8 bytes | 15 decimal digits precision | More precise scientific computations | `CREATE TABLE data (value DOUBLE PRECISION);` |
| `serial` / `bigserial` | 4 / 8 bytes | Auto-incrementing integers | Primary keys, unique row IDs | `CREATE TABLE employees (id SERIAL PRIMARY KEY);` |

#### **2. Character Types**  
| Type         | Storage | Notes | Use Case | Example |
|-------------|---------|-------|----------|---------|
| `char(n)`   | Fixed | Blank-padded | Fixed-length identifiers (e.g., country codes) | `CREATE TABLE countries (code CHAR(2));` |
| `varchar(n)` | Variable | No padding | Variable-length text (e.g., names) | `CREATE TABLE users (username VARCHAR(50));` |
| `text`      | Variable | No length limit | Storing large text data | `CREATE TABLE articles (content TEXT);` |

#### **3. Boolean Type**  
| Type     | Values | Use Case | Example |
|----------|--------|----------|---------|
| `boolean` | `TRUE`, `FALSE`, `NULL` | Status flags | `CREATE TABLE users (is_active BOOLEAN DEFAULT TRUE);` |

#### **4. Date & Time Types**  
| Type               | Storage | Format | Use Case | Example |
|--------------------|---------|--------|----------|---------|
| `date`            | 4 bytes | YYYY-MM-DD | Birthdates, event dates | `CREATE TABLE employees (dob DATE);` |
| `time [tz]`       | 8 bytes | HH:MI:SS | Time without date | `CREATE TABLE shifts (start_time TIME);` |
| `timestamp [tz]`  | 8 bytes | YYYY-MM-DD HH:MI:SS | Logging events | `CREATE TABLE logs (created_at TIMESTAMP DEFAULT NOW());` |
| `interval`        | 16 bytes | Time span | Age calculations | `CREATE TABLE projects (duration INTERVAL);` |

#### **5. UUID**  
| Type   | Notes | Use Case | Example |
|--------|-------|----------|---------|
| `uuid` | 128-bit unique ID | Securely unique identifiers | `CREATE TABLE api_keys (id UUID DEFAULT gen_random_uuid());` |

#### **6. JSON & XML**  
| Type   | Notes | Use Case | Example |
|--------|-------|----------|---------|
| `json` | Text-based JSON | Storing semi-structured data | `CREATE TABLE configs (settings JSON);` |
| `jsonb` | Optimized JSON | Faster JSON queries | `CREATE TABLE logs (metadata JSONB);` |
| `xml` | Stores XML | XML-based configurations | `CREATE TABLE documents (data XML);` |

#### **7. Arrays**  
| Type | Notes | Use Case | Example |
|------|-------|----------|---------|
| `type[]` | One/multi-dimensional arrays | Storing multiple values in one column | `CREATE TABLE products (tags TEXT[]);` |

#### **8. Special Types**  
| Type         | Notes | Use Case | Example |
|-------------|-------|----------|---------|
| `cidr` / `inet` | IP addresses | Storing and querying IPs | `CREATE TABLE servers (ip INET);` |
| `macaddr` | MAC addresses | Network devices | `CREATE TABLE devices (mac_address MACADDR);` |
| `bit(n)` | Fixed-length bit string | Binary flags | `CREATE TABLE flags (status BIT(8));` |
| `bit varying(n)` | Variable-length bit string | Flexible binary data | `CREATE TABLE users (permissions BIT VARYING(16));` |

#### **9. Geometric Types**  
| Type  | Notes | Use Case | Example |
|-------|-------|----------|---------|
| `point` | (x, y) coordinates | Geospatial data | `CREATE TABLE locations (position POINT);` |
| `line` | Infinite line | Geometric calculations | `CREATE TABLE roads (path LINE);` |
| `polygon` | Polygon | Regions, territories | `CREATE TABLE zones (area POLYGON);` |

#### **10. Monetary Type**  
| Type     | Notes | Use Case | Example |
|----------|-------|----------|---------|
| `money`  | Currency with locale formatting | Financial transactions | `CREATE TABLE payments (price MONEY);` |

#### **11. Full-Text Search Types**  
| Type         | Notes | Use Case | Example |
|-------------|-------|----------|---------|
| `tsvector` | Optimized text search format | Full-text search | `CREATE TABLE articles (body TSVECTOR);` |
| `tsquery` | Search query type | Querying text indexes | `SELECT * FROM articles WHERE body @@ to_tsquery('postgres');` |

#### **12. Composite & Custom Types**  
| Type         | Notes | Use Case | Example |
|-------------|-------|----------|---------|
| `row type` | Custom structure with multiple fields | Structured data | `CREATE TYPE address AS (street TEXT, city TEXT);` |
| `enum` | Predefined list of values | Restricting input | `CREATE TYPE status AS ENUM ('pending', 'approved', 'rejected');` |

#### **13. Range Types**  
| Type         | Notes | Use Case | Example |
|-------------|-------|----------|---------|
| `int4range`, `int8range` | Ranges of integers | Age groups, pricing tiers | `CREATE TABLE prices (amount NUMRANGE);` |
| `tsrange`, `tstzrange` | Timestamp ranges | Event durations | `CREATE TABLE reservations (booking_time TSRANGE);` |
