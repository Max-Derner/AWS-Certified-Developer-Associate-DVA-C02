```
 ___    _    __  __
|_ _|  / \  |  \/  |
 | |  / _ \ | |\/| |
 | | / ___ \| |  | |
|___/_/   \_\_|  |_|
```

## IAM Statement
A statement is the finest grain, it defines a set of actions that one resource can perform on another resource, or it can just state the actions which can be performed on a particular resource *without* naming the acting resource.  
i.e. As an EC2 instance, you may read an S3 bucket **or** as an EC2 instance, you may create a CloudWatch Stream and write to it. Or simply "you may read from S3 buckets".

## IAM Policies
A policy is a collection of statements. So, these can describe a particular way of working. So in a restaurant example, you might collect statements into a policy to describe what's needed in taking a food order. You need to speak to and listen to the customer, you need to write on a pad, and use the till to enter the order. This describes the interaction between three services to carry out a single task.  
Policies can be "user based" or "resource based", respectively that's "people acn do this stuff" ro "things can do this stuff".  

## IAM Roles
Roles define a collection of policies.  
They should be thought of in terms of the role you play in carrying out an activity.  
In a restaurant example, the food carrying role would have the order taking policy, and the fetching food from the kitchen policy. The bartender role would have policies to allow fetching garnishes for the basement, cleaning glasses, pouring drinks, etc.

## IAM Users
These are the people, not the job.  
So in our restaurant example, it's Briana, and Amy. Not chef and waitress.  

## IAM Groups
An IAM group defines a job. So back to the restaurant you might have the "front of house" job, this encompasses the food carrying role, the barista role, and the bartender role. You can then assign multiple users to one group, and one user to multiple groups. Like the waiter who fills in for the pot wash when he's out sick (sick of working a shit job for no pay more like!)  

### N.B.
IAM users can move from group to group, they can be a member of more than one group, and they have roles attached to them directly (like granting permission to the most trusted "front of house" user to get change out of the safe for that night)  

## Security
It is important to apply the principle of "least privilege". So no user or service should have any permission which it does not **absolutely need** in order to carry out it's jobs.