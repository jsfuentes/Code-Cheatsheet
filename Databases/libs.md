# Code Abstractions

## Database Driver

- raw SQL strings delievered to database with async? Rest
- connection pooling

## Query Builder

- programmatically generate dynamic queries in a much more convenient way
- generate queries for a few different SQL dialects
- **sweetspot of SQL** because clear connection to general SQL, yet dealing with fts instead of strings

## ORM

- map a record in a relational database to an object 
- Do object validation on NoSQL and create generated properties and class fields
- Learn a ORM specific interface rather than SQL
- Must update code when you update database slowing down iterations early
- Cant do everything in an ORM meaning you dip into SQL or do some inefficient code
- **sweetspot of NoSQL**, adds needed things like object validation