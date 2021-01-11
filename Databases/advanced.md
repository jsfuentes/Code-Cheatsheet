# Advanced (Postgres?)

### Transactions

Transactions group db commands to be atomic, all or nothing, and permanently recorded to disk(not dirty/in memory)

Useful for something like bank transfers where you want to ensure an amount is deducted and added or nothing 

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100.00
    WHERE name = 'Alice';
-- etc etc
COMMIT;
```

