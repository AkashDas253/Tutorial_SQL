## SELECT Command:

### Syntax:

```sql
    SELECT * | { [ DISTINCT | ALL ] value expression , ... }
        FROM { table name [ alias ] } , ...
        [ WHERE predicate ]
        [ GROUP BY { column name | integer } , ... ]
        [ HAVING predicate ]
        [ ORDER BY { column name | integer } , ... ]

[ 
    { UNION [ALL]

    SELECT * | { [ DISTINCT | ALL ] value expression , ... }
        FROM { table name [ alias ] } , ...
        [ WHERE predicate ]
        [ GROUP BY { column name | integer } , ... ]
        [ HAVING predicate ]
        [ ORDER BY { column name | integer } , ... ]
        } 
];
```

### The Elements Used in the SELECT Command:

- **value expression** : An expression that produces a value. It may include or consist of a column name.
- **table name**: A name of or synonym for a table or view.
- **alias**: A temporary synonym for table name, defined here and usable only in this command.
- **predicate**: A condition that can be true or false for each row or combination of rows from the table(s) in the FROM clause.
- **column name**: A name of a column of the table.
- **integer**: A number with no decimal point. In this case, it indicates a value expression in the SELECT clause by identifying its placement in that clause.

## The Update Commands:

### Syntax:

```sql
    UPDATE table name
    SET { column name = value expression } , ...
    [ WHERE predicate | WHERE CURRENT OF cursor name ];
```

```sql
    INSERT INTO table name [ ( column name , ... ) ]
    { VALUES ( value expression , ... ) | query };
```

```sql
    DELETE FROM table name
    [ WHERE predicate | WHERE CURRENT OF cursor name ];
```

### The Elements Used in the Update Commands:

- **cursor name**: Name of a cursor used in this program.
- **query**: A valid SELECT command.
- For other elements, see the SELECT command.

### The Symbols Used in Syntax Statements:

- **| :** Whatever precedes this symbol may optionally be replaced by whatever follows it. This is a symbolic way of saying "or".
- **{} :** Everything enclosed in curly brackets is treated as a unit for the purposes of evaluating |, ... or other symbols.
- **[] :** Everything enclosed in square brackets is optional.
- **... :** Whatever precedes this may be repeated any number of times.
- **, ... :** Whatever precedes this may be repeated any number of times with the individual occurrences separated by commas.

