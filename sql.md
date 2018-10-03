# SQL

stick to single quotes

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;

SELECT * FROM Customers
WHERE CustomerID=1
LIMIT 100;
```

## Count

```sql
SELECT COUNT(*) FROM orders;
OR
SELECT COUNT(1) FROM orders
```

### ORDER BY

```sql
ORDER BY ds DESC 
```



## CREATE

```sql
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) 
);
```

### ADVANCED HIVE?

```sql
DESCRIBE table_name; -- see the column names of the table

SHOW TABLES '\*keyword\*'; -- list all tables that contain 'keyword'

SHOW PARTITIONS table_name; -- list all the partition of the table

DROP TABLE table_name; -- erase the table

ALTER TABLE table_name_old RENAME TO table_name_new; -- rename tables
```

