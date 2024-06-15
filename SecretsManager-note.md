```
 ____                     _         __  __
/ ___|  ___  ___ _ __ ___| |_ ___  |  \/  | __ _ _ __   __ _  __ _  ___ _ __
\___ \ / _ \/ __| '__/ _ \ __/ __| | |\/| |/ _` | '_ \ / _` |/ _` |/ _ \ '__|
 ___) |  __/ (__| | |  __/ |_\__ \ | |  | | (_| | | | | (_| | (_| |  __/ |
|____/ \___|\___|_|  \___|\__|___/ |_|  |_|\__,_|_| |_|\__,_|\__, |\___|_|
                                                             |___/
```

## What be?
* Store secrets used for resources inside and outside AWS
* Set up auto-rotation
* fine-grain control over permissions and encryption with KMS
* offers cross-region replication

## Secret Types
* DB secrets
    * username & password
    * server address
    * DB name and port
* Api keys

## Security
* Everything is encrypted with KMS using the Customer Master Key (CMK).  
* Can set rotation to 30 days, 60 days, 90 days, or custom (up to 365).
* Uses Lambda to rotate keys, either pre-made or custom
* Can define IAM Policy per secret

## Secrets Manager Vs Parameter Store

| Secrets Manager | Parameter Store | 
|-----------------|-----------------|
| use for Db credentials | wide use case | 
| API keys               | config variables | 
| Rotations of keys      | license keys |