## **PostgreSQL Full-Text Search: Comprehensive Cheatsheet**  

---

## **1. Key Concepts**  
| Term | Description |
|------|-------------|
| **`tsvector`** | A text representation optimized for search. |
| **`tsquery`** | A search query format for full-text search. |
| **Lexeme** | Normalized words used for searching (ignores case and stopwords). |
| **Ranking (`ts_rank`)** | Assigns relevance scores to search results. |
| **Dictionaries** | Define rules for word normalization and stopword removal. |

---

## **2. Creating Full-Text Search Index**  
### **Example: Adding `tsvector` Column and Index**  
```sql
ALTER TABLE articles ADD COLUMN search_text tsvector;

UPDATE articles SET search_text = to_tsvector('english', title || ' ' || content);

CREATE INDEX idx_search ON articles USING GIN(search_text);
```

---

## **3. Querying Full-Text Search**  
| Method | Query |
|--------|-------|
| **Basic Search (`to_tsquery`)** | `SELECT * FROM articles WHERE search_text @@ to_tsquery('postgres');` |
| **Phrase Search (`plainto_tsquery`)** | `SELECT * FROM articles WHERE search_text @@ plainto_tsquery('full text search');` |
| **Ranked Results (`ts_rank`)** | `SELECT *, ts_rank(search_text, to_tsquery('postgres')) AS rank FROM articles ORDER BY rank DESC;` |

---

## **4. Combining Full-Text Search with Filtering**  
```sql
SELECT * FROM articles 
WHERE search_text @@ to_tsquery('database') 
AND category = 'Technology' 
ORDER BY ts_rank(search_text, to_tsquery('database')) DESC;
```

---

## **5. Optimizing Full-Text Search**  
| Technique | Description |
|-----------|-------------|
| **Use `GIN` Indexing** | Faster search for large datasets. |
| **Normalize with `to_tsvector`** | Ensures search consistency. |
| **Filter Before Searching** | Use `WHERE` clauses before full-text queries. |

---
