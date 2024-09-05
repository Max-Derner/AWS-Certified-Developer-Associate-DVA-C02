```
 _                    _         _       
| |    __ _ _ __ ___ | |__   __| | __ _ 
| |   / _` | '_ ` _ \| '_ \ / _` |/ _` |
| |__| (_| | | | | | | |_) | (_| | (_| |
|_____\__,_|_| |_| |_|_.__/ \__,_|\__,_
```

## What is it?
Serverless compute functions
* Pay for what you use
* Scale auto-magically
* Event-driven
* Independent (every event triggers its own Lambda)
* Serverless (don't you worry none about the platform it runs on)

## Price Points
* First 1M requests per month are free, then charged a $0.20 per 1M requests
* Also charged on time and memory, $0.00001667 per Gb/s (so a Lambda running with 1Gb RAM for a whole second is 1Gb/s, using 512Mb for 0.5s is 0.25Gb/s)
    * First 400,000 Gb/s per month are free

## Event Driven
Lambda can be triggered by almost anything.  
You can trigger Lambdas off the back of a change in S3 or DynamoDB, a call from a mobile app, and call through API gateway via HTTP requests.  

Which AWS services *can* trigger Lambda?
* DyanmoDB
* Kinesis
* SQS
* Application Load Balancer
* API Gateway
* Alexa
* CloudFront
* S3
* SNS
* SES
* CloudFormation
* CloudWatch
* CodeCommit
* CodePipeline
* [AND MORE!](https://docs.aws.amazon.com/lambda/latest/dg/lambda-services.html)

## Versioning
Latest version has the label `$LATEST`.  
You can create multiple versions each with their own alias (e.g. prod, test).  
Aliases can be used to shift traffic between two versions based on weights that you assign (think A/B testing).  
The ARNs have `arn:aws:lambda:<region>:<account id>:function:<name>` for `$LATEST`, and `arn:aws:lambda:<region>:<account id>:function:<name>:<version or alias>` for anything that's not `$LATEST` or that you have set up an alias for.

## Concurrency Limit
You have a "concurrent executions" limit whihc defaults to 1000, and can be manually adjusted. Going up requires AWS Support Centre request.  
There's also **reserved concurrency**, which guarantees a set number of executions, but this number also acts as a limit.

## Configuring Access For VPCs
1. Create IAM policy to allow VPC access
1. Set the VPC ID, the Subnet ID, and the Security Group ID

Lambda will then create Elastic Network Interfaces using the IPs from the subnet

## Data Storage
**Stateless**, cannot store data directly in function  
**Ephemeral**, cannot run longer than 15min  
Storing data requires you save it to data store (e.g. S3, EFS, DynamoDB)

**Native Storage** `/tmp` directory, or Lambda Layers

### `/tmp`
* 512MB default 
* 10Gb max
* persists like global variables
* vanishes with execution env, (think goes to cold storage)

### Lambda Layer
* size limit of:
    * 50MB zipped
    * 250MD unzipped
    * Though can use multiple layers
* totally persistent
* updates require totally new layer

## Environment Variables
* key-pair values
* pass values to change behaviour in one environment vs the other
* locked on version publish (once you publish your Lambda as a new version, then that version can't have it's env vars changed)

## Retries
lambda automatically performs two retries on failure

## Dead Letter Queues
Can be:
* SQS
* SNS
* Destinations
Lambda Destinations can send to one destination on success and another on failure.
Destinations can be:
* SQS
* SNS
* Lambda
* EventBridge

## Optimising
Memory and CPU are tied, cannot up one and not the other.  
Importing libraries is done on initialisation, and is a large contributor to cold-start time.

