```
 ____  ____  ____
|  _ \|  _ \/ ___|
| |_) | | | \___ \
|  _ <| |_| |___) |
|_| \_\____/|____/
```

## What do?
RDS stands for Relational Database Service, so it's just SQL in the cloud really isn't it? It's also built over the top of EC2.  
It's generally used for [Online Transaction Processing](https://en.wikipedia.org/wiki/Online_transaction_processing).  

Services to RDS:
* MicroSoft SQL Server
* Oracle
* MySQL
* PostgreSQL
* MariaDB
* Amazon Aurora (PostgreSQL & MySQL compatible)

RDS:
* is Multi-AZ (so it spans a region)
* has [Failover Capability](https://en.wikipedia.org/wiki/Failover)
* performs Automated Backups

## OLTP Vs OLAP
OTLP is **O**n**L**ine **T**ransaction **P**rocessing, you process data from transactions in real time. Like customer orders, bank transactions, etc. It's just about data processing and completing large volumes of small transactions in real-time.  

OLAP is **O**n**L**ine **A**nalytics **P**rocessing. You process complex queries to analyse data, like analysing profit over the last 3 years, or sales forecasting. It's just about doing long-running, complex analytical queries on huge amounts of data.

**N.B.** RDS is aimed at OLTP. It is not suitable for OLAP, that's more suited to something like AWS RedShift.  

## Multi-AZ
This gives you a Primary RDS instance and a Standby RDS instance. The Standby RDS instance is not visible but has data backed-up into it. If something goes wrong with the Primary, then you get automatic failover and the Standby RDS instance steps in. You only use one instance at a time.  
This can be implemented for any of the RDS services (MySQL, MariaDB, etc).  
* Exact copy in separate AZ
* Used for disaster recovery
* Automatically failover to prevent failure

## Read Replica
You can set up read replicas to speed up your services. This entails having your RDS instance duplicate it's data to another RDS instance. This read replica can be in the same AZ, or in a different one. Read replicas are not for disaster recovery like the Multi-AZ feature. You must have automatic backups enabled. You are allowed to have up to 5 read replicas for each RDS instance.  
* read only copy in same AZ, different AZ, or different region
* increases or scales read performance
* reduces load on primary RDS instance in read-heavy workloads.

## Backing up data
**Snapshots**  
User initiated manual backup that provides snapshot of storage volume attached to DB instance.  
* not automated
* no retention period (all backups kept forever)
* because it's manual, each backup is a known state

**Automated Backup**  
Enabled by default, it's just an automatic daily snapshot that happens at a time you define. Generates transaction logs to replay transactions.  
* PIT recovery down to the second within "retention period" (1-35 days)
* Full daily backup + transaction logs throughout day
* Recovers by starting at full backup then replaying transactions logs to get to point in day you specify.
* backups stored in S3 at no extra cost

## Restoration
* Restore RDS from either snapshop or automated backup
* Newly restored RDS will be a new instance with a different DNS endpoint

## Encrption
Encryption is done with KMS, and encrypts all underlying storage, automated backups, snapshots, logs, and read replicas. Encryption has to be enabled at creation, it can't be applied to an unencrypted RDS instance.  

### How to encrypt unencrypted RDS instance
Unencrypted RDS -> snapshot -> encrypted snapshot -> encrypted RDS  
Remember how restoring from snapshot creates new RDS instance.  


## RDS Proxy
Basically, it just sits between your client and your DB. It maintains a pool of active connections to your RDS instances and shares those connections between clients, which is handy in speeding up applications that are constantly opening and closing connections. It also facilitates failover speeding it up by up to 66%.

## ElastiCache
Caches frequently used data
* In memory cache
* Improves performance
* Works well for read heavy workloads

### 2 types of Elasticache

**memchaced**  
* read "mem-cash-dee"
* works well for basic object caching
* scale horizontally
* no persistance, multi-az, or failover
* super simple  

**Redis**  
* aimed at enterprise
* works for complex data-types like hashes
* has persistance, multi-az, and failover
* supports sorting and ranking data

### When to use or not use
:heavy_check_mark: heavy read loads  
:x: heavy write loads  
:x: frequently changing data (this is only a cache after all)  
:x: OLAP queries (RDS is poor choice anyway, go for RedShift)
