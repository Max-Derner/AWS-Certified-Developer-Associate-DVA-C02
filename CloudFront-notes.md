```
  ____ _                 _ _____                _   
 / ___| | ___  _   _  __| |  ___| __ ___  _ __ | |_ 
| |   | |/ _ \| | | |/ _` | |_ | '__/ _ \| '_ \| __|
| |___| | (_) | |_| | (_| |  _|| | | (_) | | | | |_ 
 \____|_|\___/ \__,_|\__,_|_|  |_|  \___/|_| |_|\__|
 ```

## What is?
It is a CDN (Content Delivery Network), which is a distributed system of servers designed to delivery your content with reduced latency and higher data transfer speeds.  
One of the geographically distributed servers is called an "Edge Location". These are distributed across the globe in order to be in closer proximity to users who may be far away from your origin server. The edge locations can cache data to serve to user more quickly.

## Some terms for the exam
* **CloudFront Origin**: The original server where your website is hosted.  
* **Edge Location**: Remote server where content is cached for rapid delivery.  
* **CloudFront Distribution**: The name given to your origin, and the configuration settings for the content you're distributing.  

## How?
With over 200 edge locations, users are routed to the closest.  
You can deliver your entire website through CloudFront.  
Optimised for AWS services like S3, EC2, ELB, and Route53 **_but_** works seamlessly with non-AWS origin servers.  

### TTL
TTL (Time To Live) is the maximum duration an object can be cached before it is automatically cleared out of the edge locations and an update must be fetched from the origin server upon the next user request.  
Default TTL is 1 day.  
You can manually clear an object from the cache before it's time but there's a charge for doing so.  

### S3 Transfer Acceleration
CloudFront can be paired with S3 Transfer Acceleration

## Options
### Price Class
You can choose which regions to employ edge locations in. All, or North America and Europe, or North America, Europe, Asia, Middle East and Africa. Not selecting all, gives a cheaper service but doesn't offer the same speeds to everyone.
### WAF
The WAF (or Web Application Firewall) can be employed to block injection attacks, DOS attacks, x-site scripting attacks, etc.
### Origin Access Identity
A special CloudFront user that can access origin bucket content, you can set up CloudFront to be the sole access to your origin (i.e. it becomes impossible to directly access the origin and all traffic goes through CloudFront).  
### Redirection
If using OAI, you can also set up CloudFront to redirect all HTTP requests to HTTPS request and even chose an SSL certificate for your CloudFront distribution to use in those HTTPS requests (the SSL cert has to be stored in AWS Certificate Manager).
### Geographic Restrictions
You have the option to set up CloudFront with an allow list or a block list to allow or block specific countries.
### Paths
You can set up CLoudFront to only cache specific files, for example large photos.

## CloudFront Allowed Methods
You may choose a group of HTTP methods to allow on your CloudFront distribution.
* **GET, HEAD** read only
* **GET, HEAD, OPTIONS** also read only
* **GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE** read and write

### A Little Explanation of Methods
| Method | Definition | Example | Read/ Write |
|--------|------------|---------|-------------|
| GET | Read data; often default method on HTTP clients | Fetch a webpage | R |
| HEAD | Inspect resource headers; like get but with no body | Read a webpage's headers | R |
| OPTIONS | Find out what HTTP methods are supported | Get list of methods | R |
| PUT | Send data to create or replace a resource (Idempotent) | Uploading form data | W |
| POST | Send data to create or replace a resource (NOT Idempotent) | Posting blog comment | W |
| PATCH | Modify a resource | Changing the content of shopping basket | W |
| DELETE | Deleting data | Removing e-mail address from mailing list | W |