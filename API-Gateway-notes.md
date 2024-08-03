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
