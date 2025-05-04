## **PostgreSQL Operators: Comprehensive Cheatsheet**  

---

## **1. Categories of Operators**  
| Category | Description |
|----------|-------------|
| **Arithmetic Operators** | Perform mathematical calculations. |
| **Comparison Operators** | Compare values and return Boolean results. |
| **Logical Operators** | Perform logical operations (`AND`, `OR`, `NOT`). |
| **Bitwise Operators** | Work on binary representations of integers. |
| **String Operators** | Manipulate text data. |
| **Pattern Matching Operators** | Match text using `LIKE`, `ILIKE`, and regular expressions. |
| **JSON Operators** | Query and manipulate JSON/JSONB data. |
| **Array Operators** | Work with array elements. |
| **Range Operators** | Handle range data types. |

---

## **2. Arithmetic Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `5 - 3` | `2` |
| `*` | Multiplication | `5 * 3` | `15` |
| `/` | Division | `5 / 3` | `1.6667` |
| `%` | Modulus (Remainder) | `5 % 3` | `2` |

---

## **3. Comparison Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `=` | Equal to | `5 = 5` | `TRUE` |
| `!=` / `<>` | Not equal to | `5 <> 3` | `TRUE` |
| `>` | Greater than | `5 > 3` | `TRUE` |
| `<` | Less than | `5 < 3` | `FALSE` |
| `>=` | Greater than or equal | `5 >= 5` | `TRUE` |
| `<=` | Less than or equal | `5 <= 3` | `FALSE` |

---

## **4. Logical Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `AND` | Both conditions must be `TRUE` | `TRUE AND FALSE` | `FALSE` |
| `OR` | At least one condition must be `TRUE` | `TRUE OR FALSE` | `TRUE` |
| `NOT` | Reverses the condition | `NOT TRUE` | `FALSE` |

---

## **5. Bitwise Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `&` | Bitwise AND | `5 & 3` | `1` |
| `|` | Bitwise OR | `5 | 3` | `7` |
| `#` | Bitwise XOR | `5 # 3` | `6` |
| `~` | Bitwise NOT | `~5` | `-6` |
| `<<` | Left Shift | `5 << 1` | `10` |
| `>>` | Right Shift | `5 >> 1` | `2` |

---

## **6. String Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `||` | String Concatenation | `'Hello' || ' World'` | `'Hello World'` |
| `LENGTH()` | Returns length | `LENGTH('Hello')` | `5` |
| `SUBSTRING()` | Extracts substring | `SUBSTRING('Hello' FROM 2 FOR 3)` | `'ell'` |

---

## **7. Pattern Matching Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `LIKE` | Case-sensitive match | `'hello' LIKE 'h%'` | `TRUE` |
| `ILIKE` | Case-insensitive match | `'Hello' ILIKE 'h%'` | `TRUE` |
| `~` | Regex match | `'hello' ~ '^h.*o$'` | `TRUE` |
| `~*` | Case-insensitive regex | `'Hello' ~* '^h.*o$'` | `TRUE` |

---

## **8. JSON Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `->` | Extracts JSON field as JSON | `json_column -> 'key'` | `{"value"}` |
| `->>` | Extracts JSON field as text | `json_column ->> 'key'` | `'value'` |
| `#>` | Extracts nested JSON field | `json_column #> '{key,subkey}'` | `{"subvalue"}` |
| `@>` | Contains JSON | `json_column @> '{"key": "value"}'` | `TRUE` |
| `<@` | Contained in JSON | `'{"key": "value"}' <@ json_column` | `TRUE` |

---

## **9. Array Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `@>` | Contains | `ARRAY[1,2,3] @> ARRAY[2]` | `TRUE` |
| `<@` | Contained in | `ARRAY[2] <@ ARRAY[1,2,3]` | `TRUE` |
| `&&` | Overlap | `ARRAY[1,2,3] && ARRAY[2,4]` | `TRUE` |
| `||` | Concatenate | `ARRAY[1,2] || ARRAY[3,4]` | `{1,2,3,4}` |

---

## **10. Range Operators**  
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `@>` | Range contains value | `'[1,5]'::int4range @> 3` | `TRUE` |
| `<@` | Value is within range | `3 <@ '[1,5]'::int4range` | `TRUE` |
| `&&` | Overlapping ranges | `'[1,5]'::int4range && '[3,7]'::int4range` | `TRUE` |
