## PostgreSQL Data Types  
 
#### Numeric Types  
| Data Type        | Description |
|-----------------|-------------|
| `smallint`      | 2-byte integer (-32,768 to 32,767) |
| `integer` (`int`) | 4-byte integer (-2,147,483,648 to 2,147,483,647) |
| `bigint`        | 8-byte integer (-9 quintillion to 9 quintillion) |
| `decimal(p,s)` (`numeric(p,s)`) | User-defined precision (p) and scale (s) |
| `real`          | 4-byte floating-point number |
| `double precision` | 8-byte floating-point number |
| `serial`        | Auto-incrementing 4-byte integer |
| `bigserial`     | Auto-incrementing 8-byte integer |

#### Character Types  
| Data Type        | Description |
|-----------------|-------------|
| `char(n)`       | Fixed-length string (padded with spaces) |
| `varchar(n)`    | Variable-length string with limit `n` |
| `text`          | Variable-length string (unlimited) |

#### Date/Time Types  
| Data Type         | Description |
|------------------|-------------|
| `date`          | Stores only date (YYYY-MM-DD) |
| `time`          | Stores only time (HH:MI:SS) |
| `timestamp`     | Stores date and time without time zone |
| `timestamptz` (`timestamp with time zone`) | Stores date and time with time zone awareness |
| `interval`      | Stores time duration (e.g., '1 year 2 months') |

#### Boolean Type  
| Data Type | Description |
|-----------|-------------|
| `boolean` | `true`, `false`, or `NULL` |

#### UUID Type  
| Data Type | Description |
|-----------|-------------|
| `uuid`    | Universally Unique Identifier (128-bit value) |

#### JSON Types  
| Data Type | Description |
|-----------|-------------|
| `json`    | Stores JSON data as a text-based representation |
| `jsonb`   | Stores JSON data in binary format with indexing support |

#### Array Types  
| Data Type       | Description |
|----------------|-------------|
| `ARRAY`        | Stores an array of any PostgreSQL data type |

#### Geometric Types  
| Data Type | Description |
|-----------|-------------|
| `point`   | (x, y) coordinate |
| `line`    | Infinite line |
| `lseg`    | Line segment |
| `box`     | Rectangular box |
| `path`    | Open or closed path |
| `polygon` | Polygon |
| `circle`  | Circle with center and radius |

#### Network Address Types  
| Data Type | Description |
|-----------|-------------|
| `cidr`    | IPv4 or IPv6 network |
| `inet`    | IPv4 or IPv6 address |
| `macaddr` | MAC address |
| `macaddr8` | MAC address (EUI-64 format) |

#### Bit String Types  
| Data Type      | Description |
|---------------|-------------|
| `bit(n)`      | Fixed-length bit string |
| `bit varying(n)` (`varbit(n)`) | Variable-length bit string |

#### XML Type  
| Data Type | Description |
|-----------|-------------|
| `xml`     | Stores XML data |

#### Full-Text Search Types  
| Data Type          | Description |
|-------------------|-------------|
| `tsvector`       | Lexeme representation for text search |
| `tsquery`        | Query format for text search |

#### Range Types  
| Data Type            | Description |
|---------------------|-------------|
| `int4range`        | Range of `integer` values |
| `int8range`        | Range of `bigint` values |
| `numrange`         | Range of `numeric` values |
| `daterange`        | Range of `date` values |
| `tsrange`          | Range of `timestamp` values |
| `tstzrange`        | Range of `timestamptz` values |

#### Composite Types  
| Data Type | Description |
|-----------|-------------|
| `rowtype` | Stores multiple fields like a table row |

#### Enumerated Types  
| Data Type | Description |
|-----------|-------------|
| `enum`    | User-defined set of values |

#### Custom Types  
| Data Type | Description |
|-----------|-------------|
| `domain`  | User-defined constraint on an existing type |
| `composite` | Custom type combining multiple columns |

#### Large Object Type  
| Data Type | Description |
|-----------|-------------|
| `oid`     | Object Identifier (for large objects) |

---