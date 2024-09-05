```
    _    ____ ___    ____       _                           
   / \  |  _ \_ _|  / ___| __ _| |_ _____      ____ _ _   _ 
  / _ \ | |_) | |  | |  _ / _` | __/ _ \ \ /\ / / _` | | | |
 / ___ \|  __/| |  | |_| | (_| | ||  __/\ V  V / (_| | |_| |
/_/   \_\_|  |___|  \____|\__,_|\__\___| \_/\_/ \__,_|\__, |
                                                      |___/ 
```

## What is?
Publish, maintain, monitor, and secure APIs at any scale.  
Supports:
* **RESTful APIs**: optimised for stateless, serverless workloads  
* **Websocket APIs**: for realtime, two-way, stateful communication (e.g. chat apps)  
* Multiple endpoints and targets, can have lots of different endpoints which each point to a different target.
* Multiple versions, maintain many different versions (e.g. dev, test, prod)
* CloudWatch, for all those logs about API calls, latencies, and error rates.
* Throttling, to dampen traffic spikes, or prevent DOS attacks.

API Gateway gives a single endpoint for all your client traffic. From API gateway, you can then feed off to various services such as Lambda, EC2, Elastic Beanstalk, DynamoDB, and Kinesis.

## RESTful APIs
* Stands for **Re**presentational **S**tate **T**ransfer.
* Stateless
* Supports JSON

## importing 
You can import your own API definition files into API GW as a quick way to set up. You have to use the industry standard `OpenAPI` (formerly `Swagger`)

## legacy
Today's standard is REST but API GW supports SOAP - a legacy format that passes XML straight through to your servers. AWI GW can also be set up to convert XML to JSON for you.

## mocks
API GW can be used to create a mock endpoint, to allow you to fake a service until you're ready to use the real thing

## stages
API GW can be set up to essentially have different versions like dev, prod, v3, etc

You get stage variables too. So, these act like environment variables and can change the behaviour of your API. Stage variables can configure which endpoint to use
