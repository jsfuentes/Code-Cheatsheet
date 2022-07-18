# Aggregate

When you use GROUP_BY, you can only select aggregates or columsn in the GROUP_BY 

#### Count

- `COUNT(*)` /`COUNT(1)`counts all rows
- `COUNT(column)` counts non-NULLs only

```sql
SELECT COUNT(*) FROM orders GROUP BY ds;
```

#### Max

Even works for strings where later in the alphabet is more

#### Min

Even works for strings where later in the alphabet is more