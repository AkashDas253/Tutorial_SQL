### PostgreSQL Character Data Types  

#### Character Types  
Used to store textual data.  

| Data Type   | Size | Behavior | Notes |
|------------|------|----------|------------------------------------------------|
| `char(n)`  | Fixed | Fixed-length, padded with spaces | Best for storing fixed-size codes like country codes. |
| `varchar(n)` | Variable | Variable-length, up to `n` characters | Efficient for varying text lengths with a defined limit. |
| `text` | Variable | Unlimited length | Preferred for long, unrestricted text storage. |

#### Key Differences  
| Feature | `char(n)` | `varchar(n)` | `text` |
|---------|----------|-------------|-------|
| Storage | Fixed-length | Variable-length | Variable-length |
| Padding | Pads with spaces | No padding | No padding |
| Performance | Slightly slower due to padding | Optimized for length variation | Optimized for long text |
| Use Case | Fixed-size identifiers | General text with length limits | Large text fields |

#### Usage Scenarios  
| Scenario | Recommended Type |
|----------|----------------|
| Storing fixed-length identifiers (e.g., country codes) | `char(n)` |
| Storing names or descriptions with length restrictions | `varchar(n)` |
| Storing long text such as articles or logs | `text` |

---