## **PostgreSQL XML Support: Comprehensive Cheatsheet**  

---

## **1. XML Data Type in PostgreSQL**  
| Data Type | Description |
|-----------|-------------|
| **XML** | Stores XML data in a structured format with validation. |

---

## **2. Creating a Table with XML Columns**  
```sql
CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    details XML
);
```

---

## **3. Inserting XML Data**  
```sql
INSERT INTO books (details) 
VALUES ('<book><title>PostgreSQL Guide</title><author>John Doe</author></book>');
```

---

## **4. Querying XML Data**  
| Method | Query |
|--------|-------|
| **Retrieve Entire XML** | `SELECT details FROM books;` |
| **Extract Specific XML Element (`xpath()`)** | `SELECT xpath('/book/title/text()', details) FROM books;` |

---

## **5. Modifying XML Data**  
| Operation | Query |
|-----------|-------|
| **Update XML Column** | `UPDATE books SET details = '<book><title>New Title</title><author>John Doe</author></book>' WHERE id = 1;` |

---

## **6. XML Functions**  
| Function | Description |
|----------|-------------|
| `xmlconcat()` | Concatenates multiple XML fragments. |
| `xmlelement(name, value)` | Creates an XML element. |
| `xmlattributes()` | Adds attributes to an XML element. |
| `xpath()` | Queries XML data using XPath expressions. |

### **Example: Creating XML Elements**
```sql
SELECT xmlelement(name book, xmlattributes('12345' AS isbn), 'PostgreSQL Guide');
```
