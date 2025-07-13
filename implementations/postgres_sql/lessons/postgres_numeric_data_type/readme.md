### PostgreSQL Numeric Data Types  

#### Integer Types  
Used for whole numbers without fractions.  

| Data Type  | Size  | Range | Notes |
|------------|------|----------------------------------|------------------------------------------------|
| `smallint` | 2 bytes | -32,768 to 32,767 | Suitable for small numeric values to save space. |
| `integer` (`int`) | 4 bytes | -2,147,483,648 to 2,147,483,647 | Default integer type for general use. |
| `bigint` | 8 bytes | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | Used for large numbers requiring more storage. |
| `serial` | 4 bytes | 1 to 2,147,483,647 | Auto-incrementing integer (creates sequence). |
| `bigserial` | 8 bytes | 1 to 9,223,372,036,854,775,807 | Auto-incrementing large integer. |

#### Decimal and Floating-Point Types  
Used for precise or approximate numeric values.  

| Data Type  | Size  | Precision | Range | Notes |
|------------|------|----------------|---------------------------|------------------------------------------------|
| `decimal(p,s)` (`numeric(p,s)`) | Variable | User-defined (p = total digits, s = decimal places) | Unlimited | Provides exact precision, used for financial calculations. |
| `real` | 4 bytes | 6 decimal digits | ± 1.18 × 10⁻³⁸ to ± 3.4 × 10³⁸ | Approximate precision, used for scientific data. |
| `double precision` | 8 bytes | 15 decimal digits | ± 2.23 × 10⁻³⁰⁸ to ± 1.8 × 10³⁰⁸ | Higher precision floating-point number. |

#### Auto-Incrementing Types  
- **`serial` and `bigserial`** automatically create an associated sequence to generate unique values.  
- These are shorthand for:  
  ```sql
  serial     -> integer NOT NULL DEFAULT nextval('sequence_name')
  bigserial  -> bigint NOT NULL DEFAULT nextval('sequence_name')
  ```

#### Usage Scenarios  
| Scenario | Recommended Type |
|----------|----------------|
| Counting rows in a table | `serial` or `bigserial` |
| Financial calculations requiring exact precision | `numeric` (`decimal`) |
| Storing large numbers such as timestamps | `bigint` |
| Scientific computations with approximate precision | `double precision` |

---