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

## S3 Object Breakdown
* **Key** name of object
* **Value** object itself
* **Version ID** shows up when versioning objects and allows reference to older versions
* **Metadata** additional info (e.g. content-type, last modified, etc)

**N.B.** The largest object you can upload in a single `PUT` is 5Gb. When uploading objects larger than 100Mb, you should consider a multi-part upload.

## Security
* optional Server-side encryption
* Access Control Lists (ACLs) add a white list to the bucket as a whole, or to individual items within the bucket
* Can enforce encryption:
    * Deny requests that do not include `x-amz-server-side-encryption`
    * Deny requests that do not use `aws:SecureTransport` to enforce use of `HTTPS/SSL`

**Default settings:** bucket owner is the only one with access  
**Bucket policies:** can apply what is basically an IAM policy to entire bucket  
**Access Control Lists:** or ACLs. These apply to individual items within the bucket, allowing super fine grain control.  
**Access Logs:** You can set up logging for who reads, writes, and deletes what in the S3 bucket.  

## Storage Classes


**N.B.** S3 buckets have unlimited storage but each object has a max size of 5Tb

| Bucket Type | Azs | Min Storage Duration | Min Object Size | Retrieval Time | Charged Access | Examples |
|-|-|-|-|-|-|-|
| S3 Standard| >= 3 | None | None | Instant | No | websites, content distribution, mobile and gaming apps, and big data analytics|
| S3 Standard-Infrequent Access (S3-IA) | >= 3 | 30 days | 128KB | Instant | Yes | long-term storage, backups, disaster recovery files |
| S3 One Zone Infrequent Access | 1 | 30 days | 128KB | Instant | Yes | long lived, infrequently accessed, non-critical data |
| S3 Glacier Instant Retrieval | >= 3 | None | 128KB | Instant | Yes | Media asset workflows, Healthcare information archiving, Scientific data analytics |
| S3 Glacier Flexible Retrieval | >= 3 | 90 days | 128KB | Configurable between 1 min to 12 hrs | Yes | backup and disaster recovery use cases when large sets of data occasionally need to be retrieved in minutes, without concern for costs |
| S3 Glacier Deep Archive | >= 3 | 180 days | 128KB | 12 hours | Yes | Ideal alternative to magnetic tape libraries |
| Intelligent-Tiering | >= 3 | 30 days | 128KB | Swaps automatically to optimise cost | No | Unknown and unpredictable access patterns |

**N.B.** "Min Storage Duration" and "Min Object Size" does not mean you can't remove an object sooner or store an object smaller, it just means AWS will bill you as if you did store for that time or that size.


## Encryption

In transit:
* SSL/TLS & HTTPS

At rest (server-side encryption):
* SSE-S3 - S3 managed keys (**S3 default setting**)
* SSE-KMS - KMS keys
* SSE-C - customer managed keys 

At rest (client-side encryption):
* User encrypts files before uploading

## CORS
Cross-Origin Resource Sharing policies can be set up for S3 buckets. You will need to do this to share resources from one bucket to another (e.g. static website setup pulling from a separate bucket).  

## S3 Transfer Acceleration
Is what it sounds like. It enables faster and still secure transfers transfers over long distances.