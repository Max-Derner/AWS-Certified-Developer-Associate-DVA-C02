```
 ____ _____ 
/ ___|___ / 
\___ \ |_ \ 
 ___) |__) |
|____/____/ 
```

## What be?
* Object based storage (not suitable for OS or DB)
* Secure
* Scalable (unlimited storage)
* Max item size of 5TB
* Universal namespace (every bucket needs unique name)
* homogenous URLS (https://**\<bucket-name\>**.s3.**\<region\>**.amazonaws.com/**\<item-name\>**)
* key-value store (name and file)
* versioning
* add meta-data
* designed for availability and durability
* different storage tiers at different prices
* lifecycle management (define rules to move older items to cheaper storage tier)

## Security
* optional Server-side encryption
* Access Control Lists (ACLs) add a white list to the bucket as a whole, or to individual items within the bucket

## Storage Classes
* S3 Standard
    * High availability and durability, kept across at least 3 AZs
    * Designed for frequent access
    * e.g. websites, content distribution, mobile and gaming apps, and bid data analytics
    * 99.99% availability & 99.999999999% durability
* S3 Standard-Infrequent Access (S3-IA)
    * rapid access when needed
    * pay per GB to access data
    * minimum storage duration of 30 days
    * e.g. long-term storage, backups, disaster recovery files
    * 99.9% availability  & 99.999999999% durability
* S3 One Zone-Infrequent Access
    * only stores in one AZ
    * costs 20% less than S3-IA
    * minimum storage of 30 day
    * ideal for long lived, infrequently accessed, non-critical data
    * 99.5% availability  % 99.999999999%
* S3 Glacier Instant Retrieval
    * Long-lived data that is accessed a few times per year
    * lowest cost instant retrievals
    * 128 KB minimum object size
    * 99.9% availability  & 99.999999999% durability
* S3 Glacier Flexible Retrieval
    * configurable retrieval times of minutes to hours
    * 99.99% availability & 99.999999999% durability
* S3 Glacier Deep Archive
    * retrieval times of 12 hours
    * 99.99% availability & 99.999999999% durability
* Intelligent-Tiering
    * has two tiers under the hood (frequent & infrequent access)
    * automatically swaps between them in an attempt to save you money

**N.B.** Any infrequent access storage class has a data retrieval charge

| Bucket Type | Azs | Min Storage Duration | Min Object Size | Retrieval Time | Charged Access | Examples |
|-|-|-|-|-|-|-|
| S3 Standard| >= 3 | None | None | Instant | No | websites, content distribution, mobile and gaming apps, and big data analytics|
| S3 Standard-Infrequent Access (S3-IA) | >= 3 | 30 days | 128KB | Instant | Yes | long-term storage, backups, disaster recovery files |
| S3 One Zone Infrequent Access | 1 | 30 days | 128KB | Instant | Yes | long lived, infrequently accessed, non-critical data |
| S3 Glacier Instant Retrieval | >= 3 | None | 128KB | Instant | Yes | Media asset workflows, Healthcare information archiving, Scientific data analytics |
| S3 Glacier Flexible Retrieval | >= 3 | 90 days | 128KB | Configurable between 1 min to 12 hrs | Yes | backup and disaster recovery use cases when large sets of data occasionally need to be retrieved in minutes, without concern for costs |
| S3 Glacier Deep Archive | >= 3 | 180 days | 128KB | 12 hours | Yes | Ideal alternative to magnetic tape libraries |
| Intelligent-Tiering | >= 3 | 30 days | 128KB | Swaps automatically to optimise cost | No | |

**N.B.** "Min Storage Duration" and "Min Object Size" does not mean you can't remove an object sooner or store an object smaller, it just means AWS will bill you as if you did store for that time or that size.

