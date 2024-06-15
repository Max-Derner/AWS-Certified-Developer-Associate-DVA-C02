```
  ____ _     ___
 / ___| |   |_ _|
| |   | |    | |
| |___| |___ | |
 \____|_____|___|
 ```
 ## Pagination & Timed Out Errors
 In cases where CLI call to get items down from your infrastructure are resulting in "timed out" errors, then you can paginate it better.  
 So, you can simply use `--page-size` to set a lower page size (default of 1000), this makes more API calls which are also smaller, and helps prevent timing out.

 