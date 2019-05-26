# Databases

Can have a master slave distrubuting reads

Can have sharding handle different parts of requests

# SQL VS NoSQL

SQL

- battle-tested and refined
- better consistency/ACID(Atomic Consisent Isolation Durability)

NoSQL

- easier to use
- more scalable(not a real problem until massive)
- faster joins
- 

## SQL

**SQL** has tables and a schema managed by a **RDMS**(Relational Database Management System)

- battle-tested and refined
- better consistency/ACID(Atomic Consisent Isolation Durability)

## NoSQL

- easier to use
- more scalable(not a real problem until massive)
- faster joins
- no complex transactions or constraints on data
- BASE(Basically Available Soft-state Eventual Consistency) trades C and I for availability, graceful degradation, and performance

#### Types of SQL

- Key value store i.e Memcached, Redis

- Tabular i.e BigTable(Google)

- Document Oriented i.e Mongodb

### Data Warehousing

Hadoop is good for huge(PB) analytics using distrubuted file systems based on GFS(google file system) from paper in 2003 

Map Reduce is used to do analytics

Hive Query Language is used to turn SQL queries into Map Reduce Jobs