```
 ____             _         ____ _____ 
|  _ \ ___  _   _| |_ ___  | ___|___ / 
| |_) / _ \| | | | __/ _ \ |___ \ |_ \ 
|  _ < (_) | |_| | ||  __/  ___) |__) |
|_| \_\___/ \__,_|\__\___| |____/____/ 
```

## What be?
Route 53 is the DNS service at AWS.  

You can map a domain name to an:
* EC2 instance
* Elastic Load Balancer
* S3 Bucket
* ...and more!

## Terminology
**Hosted Zone** - A file of your DNS records  
**Alias** - routes traffic addressed for the zone apex, or top of the namespace, and sends it to an AWS resource.  
**A Record** - (that's an "A Record") routes traffic to a resource using an IPv4 address
