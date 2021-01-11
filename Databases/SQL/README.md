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

## Basic Query

#### ORDER BY / SORT

```sql
ORDER BY ds DESC 
```

#### MULTI TABLE

```sql
SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE c.CustomerName="Around the Horn";
```

#### WHERE

```sql
 WHERE Country IN ('USA', 'UK', 'Japan')
```

```sql
WHERE category_id IS NOT NULL
AND ds = '2018-01-10'
AND timestamp >= 9413215908
```

AND has precedence over OR

#### INSERT

```sql
INSERT INTO table2 (column1, column2, column3, ...)
SELECT column1, column2, column3, ...
FROM table1
WHERE condition;
```

#### Update

The where clause will determine how many to update, omitted means all

```sql
UPDATE Customers
SET ContactName='Juan'
WHERE Country='Mexico';
```

### ADVANCED

Limit and Offset to do pagination

#### JOINS

- **(INNER) JOIN**: Returns records that have matching values in both tables
- **LEFT (OUTER) JOIN**: Return all records from the left table, and the matched records from the right table
- **RIGHT (OUTER) JOIN**: Return all records from the right table, and the matched records from the left table
- **FULL (OUTER) JOIN**: Return all records when there is a match in either left or right table

```sql
SELECT *
FROM Orders
LEFT JOIN Customers
ON Orders.CustomerID = Customers.CustomerID;
```

#### CASE

```sql
SELECT player_name,
       weight,
       CASE WHEN weight > 250 THEN 'over 250'
            WHEN weight > 200 THEN '201-250'
            WHEN weight > 175 THEN '176-200'
            ELSE '175 or under' END AS weight_group
  FROM benn.college_football_players
```

Executed in order as shown 

## Table Structure

#### CREATE

```sql
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) 
);
```

#### DELETE

Permanently deletion, be careeefullll

```sql
DROP TABLE Shippers;
```

```sql
ALTER TABLE "public"."_students" ADD COLUMN "race" int4
```

### ADVANCED HIVE?

95% SQL syntax, but can query Hadoop turning HiveQL into Map Reduce Jobs 

#### Explode

Make a new row for each list entry

adid_list is an Array of ints 

pageid	|	adid_list			becomes=>	pageid	|	adid

1		|	[1,2]						1		|	1

​										1		|	2	

```sql
SELECT pageid, adid
FROM pageAds LATERAL VIEW explode(adid_list) adTable AS adid;
```

#### HIVE COMMAND LINE

```sql
DESCRIBE table_name; -- see the column names of the table

SHOW TABLES '\*keyword\*'; -- list all tables that contain 'keyword'

SHOW PARTITIONS table_name; -- list all the partition of the table

DROP TABLE table_name; -- erase the table

ALTER TABLE table_name_old RENAME TO table_name_new; -- rename tables
```

