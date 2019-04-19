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

Can install with brew `brew install postgresql`

`postgres -V`

`psql` to enter cml

## Psql

- `\du` to see users installed 

- `\list`: lists all the databases in Postgres
- `\connect`: connect to a specific database
- `\dt`: list the tables in the currently connected database

