```
 ___    _    __  __
|_ _|  / \  |  \/  |
 | |  / _ \ | |\/| |
 | | / ___ \| |  | |
|___/_/   \_\_|  |_|
```

## IAM Policies
A policy is the finest grain, it defines a specific permission between two services.  
i.e. As an EC2 instance, you may read an S3 bucket **or** as an EC2 instance, you may create a CloudWatch Stream and write to it.

## IAM Roles
Roles define a collection of policies.  
They should be thought of in terms of the role you play in carrying out an activity.  
In a restaurant example, the food carrying role would have access to customers, and to the interface of the kitchen, but would not have access to the inside of the kitchen. A coffee maker role would have access to all of the coffee machine. Etc  

## IAM Users
These are the people, not the job.  
So in our restaurant example, it's Briana, and Amy. Not chef and waitress.  

## IAM Groups
These are pools of IAM Users, to which you can attach various roles.  
So in the restaurant example, there's a waiter role with "food carrying" role, and "coffee maker" role attached to it.  

### N.B.
IAM users can move from group to group, they can be a member of more than one group, and they have roles attached to them directly.  

## Security
It is important to apply the principle of "least privilege". So no user or service should have any permission which it does not **absolutely need** in order to carry out it's jobs.