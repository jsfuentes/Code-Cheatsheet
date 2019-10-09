# RDS(Relational DB Service)

There is Amazon RDS for installing specific DB 

The only thing you need to do its managing schema and managing the data. Amazon doesn't touch data 

You do need to provision scale

Use an EBS Volume as Storage

See Aurora for AWS managed

Can host multiple databases and such on one instance

## Connection

Need host, port, and username and password to connect with some dbtool like tableplus and pgadmin

Code connects also need database name

## Creation

Set admin user and password

1) Select Engine(aurora, mysql, postgres)

2) use case: high availbility or cheaper

3) DB Details: size , initial settings about username and password

4) Advanced: VPC, Security, Encryption, backup, monitoring, logs 

Read Replicas node 

Secondary Host would handle load in case of failure}

No charge for backups up to 100%

Encryption at rest free, done at volume level with RDS connecting with KMS so app changes

#### Multi-AZ(Avaliability Zones)

- allow great availiability during maintence and fails
- fallover takes about 1-2 minutes
- Writes go to both and twice the cost
- Backups improved 

#### Read Replicas

- part of instance and only handle read queries to offload traffic from main
- "eventually consistent" so writes on primary, then asyncronously updates the replica, so query could get stale data
- Check replication lag in the replication tab of the master
- Create from the options of any database instance, promote to a standalone instance from the options of the replica thing(irreversible)

#### Automated Backups

EBS has a snapshot stored everyday, incremental snapshots only store difference, brief I/o suspension to uptown few minutes

Transaction Logs are then stored every 5 minutes so you can then get your db to any pt in time :0

##### Restoring Snapshot

Must create a new instance

Snapshots can be sent to new region

### Scaling

Vertical scale by modifying db to add storage or instance type(downtime), multi-az has minimal downtime

- t2.small to medium took about 5 minutes, multi a-z had about a minute of downtime as fallover kicked in 

Horizontal scale by adding read replicas