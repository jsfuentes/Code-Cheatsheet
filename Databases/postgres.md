# Postgres

SQL DB with:

- Streaming replication
- Schemas
- User-defined objects like operators, data types, and functions
- Nested transactions
- Table inheritance
- Partitioning
- Several unusual data types, like Money, Geometry, IP addresses, JSON, and data ranges.
- Can execute stored procedures in over a dozen programming languages, including Java, Perl, Python, Ruby, and C/C++.

## Setup

Can install with brew `brew install postgresql`, follow instructions onscreen(`brew services start postgresql` & `initdb  /usr/local/var/postgres` )

`postgres -V`

`psql` to enter cml

## Types

| **Character Types**                  | **Description**            |
| ------------------------------------ | -------------------------- |
| character varying(*n*), varchar(*n*) | variable-length with limit |
| character(*n*), char(*n*)            | fixed-length, blank padded |
| text, varchar                        | variable unlimited length  |

If you do not specify the n integer for the `varchar` data type, it behaves like the `text` data type. The performance of the `varchar` (without n) and `text` are the same.

## Psql

- `\du` to see users installed 

- `\list`: lists all the databases in Postgres
- `\connect`: connect to a specific database
- `\dt`: list the tables in the currently connected database

