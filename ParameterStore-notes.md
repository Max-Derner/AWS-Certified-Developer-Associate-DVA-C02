```
 ____                                _              ____  _
|  _ \ __ _ _ __ __ _ _ __ ___   ___| |_ ___ _ __  / ___|| |_ ___  _ __ ___
| |_) / _` | '__/ _` | '_ ` _ \ / _ \ __/ _ \ '__| \___ \| __/ _ \| '__/ _ \
|  __/ (_| | | | (_| | | | | | |  __/ ||  __/ |     ___) | || (_) | | |  __/
|_|   \__,_|_|  \__,_|_| |_| |_|\___|\__\___|_|    |____/ \__\___/|_|  \___|
```

## What be?
It's just a place to keep secret stuff like passwords, license keys, DB connection info. All the secrets you don't want hardcoded into repo.  
This is the kinda stuff that gets bootstrapped by a bootstrap script.

**N.B.** It's kept under Systems Manager in the AWS Console.

## How do?
Well it's just key value pairs, that's it.

## Tiers
**Standard** This is free, it can keep up to 10,000 4KB parameters at no charge.  
**Advanced** This is not free, it can keep over 10,000 8KB parameters.

## Types
* String
* StringList (csv style)
* SecureString (encrypted with KMS)

## Tags
Each parameter can have tags, and tags are just key value pairs


## How easy?
It's integrated into:
* EC2
* CloudFormation
* Lambda
* CodeBuild
* CodePipeline
* CodeDeploy


## Secrets Manager Vs Parameter Store

| Secrets Manager | Parameter Store | 
|-----------------|-----------------|
| use for Db credentials | wide use case | 
| API keys               | config variables | 
| Rotations of keys      | license keys |
