# Aurora

Why not RDS:

- SQL, Transacations, Caching, Storage, Logging are in every A-Z and monolithic stack that means all are slow

Why:

- No unfront allocation of storage
- Faster
- Self-healing, and automatic fallover to replicas so great

RDS cloud optimizes it to split up the levels , and has a shared storage level

Compatible with MySQL and Postgres

DB Cluster consists of more DB instances and a cluster volume

1. Primary DB, in primary region
2. Aurora Replica, automatically failover here

DB connections

Cluster endpoints is only one that can do writes

One Reader endpoint that provides read 

Custom endpoints allows one group of instances

Instance endpoints specify db instance

## Depth

Aurora has a storage layer with constant monitoring

Each A-Z will have multiple data blocks and if anyone is ever corrupted it will be self healing

Postgres 2-3x and MySQl 5-6x

