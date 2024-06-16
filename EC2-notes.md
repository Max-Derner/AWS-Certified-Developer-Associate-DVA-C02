```
 _____ ____ ____  
| ____/ ___|___ \  
|  _|| |     __) |  
| |__| |___ / __/  
|_____\____|_____|  
```

## EC2 Instance Pricing Styles
**On demand** - pay for what you use, still one of the cheap-ish options  

**Reserved** - declare a usage and get up to 72% discount  
* Standard RIs - Cannot change size once bought in  
* Convertible RIs - Option to scale up or down after buy in  
* Scheduled RIs - Only spins up for specific windows  

**Spot** - if no one is using the EC2 instance, you can hop on for up to 90% discount but if the demand increases price past what you're willing to pay then you get shut down (great for crypto mining)  
This is like shorting the market.

**Dedicated** - buy a dedicated server (most expensive)  
* Use whenever you can't allow multi-tenant virtualisation  
* Can be purchased as "on-demand" or "reserved"

## EC2 Instance Types
There are a variety of instance types that determine the underlying hardware. Don't you stress none mind, 'cause know what they are ain't on the test. Just know that there are different horses for different courses.  

## EC2 EBS Volumes
**EBS** stands for Elastic Block Store.  
It's basically a filesystem you can attach to your EC2 instance.  
Gets automatically replicated across availability zones, to protect against hardware failure.  
It's scalable to dynamically increase or decrease capacity with no downtime.  

### Types
[Docs](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volume-types.html)  
* "**gp2/gp3**" is general purpose SSD. top of 16kIOPS  
* "**io1/io2**" is provisioned IOPS SSD (it be fast, think databases and shit) top of 64kIOPS  
* "**io2 Block Express**" is a SAN (Storage Area Network), this is the biggest and most performant. top of 256kIOPS  
* "**st1**" is a throughput optimised HDD (it's a fricken disk!) it can cheaply store tonnes of data. **Cannot** be a boot volume! top throughput of 500MB/s  
* "**sc1**" described as a cold HDD (lowest cost, super slow). Also **cannot** be a boot volume! top throughput of 250MB/s  

## Elastic Load Balancer
Load balancer distributes traffic across a group of servers.  
* **Application Load Balancer** handles HTTP and HTTPS
* **Network Load Balancer** handles TCP (high performance)
* **Classic Load Balancer** handles HTTP, HTTPS, and TCP
* **Gateway Load Balancer** balances for 3rd party apps in AWS

These all mask the IP address, so if you want to know where something has come 
from, you need to look at the **X-Forawrded_For** header, this preserves that IP address.

**Common Errors**  
*504 Gateway Timeout*: The target has failed to respond to the balancer in a timely fashion.

## The OSI Model (not on exam)
The OSI model describes a network

**Layer 7** *Application:* What the end user sees, HTTP, web browsers  
**Layer 6** *Presentation:* Data is now in usable format, Encryption, SSH  
**Layer 5** *Session:* Maintains connections and sessions  
**Layer 4** *Transport:* Transmits data via TCP and UDP  
**Layer 3** *Network:* Logically routes packets based on IP  
**Layer 2** *Data Link:* Physically transmits data based on MAC  
**Layer 1** *Physical:* Transmits bit and bytes over physical devices  

## Using EC2 As A Website
### Configure EC2 
Set network settings to allow inbound HTTP traffic across port 80 with TCP protocol.  
Configure EC2 Security Group to specify a subnet (this pins your API down to a specific availability zone) and name it.  

Configure EC2 instance for to act as a web server.
e.g. you can add the following to "User Data" (it's the start up script, terrible bloody name)
```
#! /bin/bash
yum update -y
yum install httpd -y  # Install Apache Server
echo -e "<html><body><h1>Hello World! Oh, hi Max!</h1></body></html>" > var/www/html/index.html  # Echo into default dir for server
systemctl start httpd  # Start server
systemctl enable httpd  # Enable server
```


### Create Application Load Balancer:
* Internet facing
* IPV4
* select VPC
* set Mappings to the same availability zone the EC2 API is in and one extra
* Select security group created earlier
* Set Listeners to HTTP over port 80
* Under listeners, select "create target" (goes to new tab)
    * set target type to "Instance"
    * Protocol HTTP
    * Port 80
    * Under health checks enter index.html
    * Click next
    * Select instance and click "Include As Pending Below"
    * click "Create Target Group"
* Back with the Load Balancer config, refresh the target groups
* select your target group
* click "Create Load Balancer"

### Linking through Route53
* go to hosted zone (created auto magically when registering a domain)
* create an "A" record
* select alias
    * set "alias to" to Application Load Balancer
    * set region to match Load Balancer
    * select Load Balancer
* use simple routing

### Result
We have the following set up:  
client --> route53 --> load balancer --> EC2


## Image Builder
Allows the weak of mind to easily create images, just learn Docker mate.  
It does allow for automating security updates and whatnot quite nicely and easily to be fair.  

### How do?
1. Choose base OS
1. Define software to install
1. Run tests (i.e. does it boot correctly?)
1. Distribute to various regions

### Terminology
**image pipeline** defines the config and E2E process of building images.  
**image recipe** defines base image and installed software.  
**build components** defines only the software.  
**AMI** this is an "Amazon Machine Image".  
So, an AMI is just an image. Then an "EC2 instance" is an actual container.

## AMIs

### Regional
AMIs are regional, if you want to use one in another region, you need to copy it out. Some places don't allow encryption (like Russia).  

Rules for encryption and copying:
* encrypted -> encrypted :heavy_check_mark:
* unencrypted -> unencrypted :heavy_check_mark:
* unencrypted -> encrypted :heavy_check_mark: (**but you must specify that you want encryption as it is not default behaviour**)
* encrypted -> unencrypted :x:








