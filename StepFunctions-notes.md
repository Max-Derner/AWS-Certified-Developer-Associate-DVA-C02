```
 ____  _               _____                 _   _                 
/ ___|| |_ ___ _ __   |  ___|   _ _ __   ___| |_(_) ___  _ __  ___ 
\___ \| __/ _ \ '_ \  | |_ | | | | '_ \ / __| __| |/ _ \| '_ \/ __|
 ___) | ||  __/ |_) | |  _|| |_| | | | | (__| |_| | (_) | | | \__ \
|____/ \__\___| .__/  |_|   \__,_|_| |_|\___|\__|_|\___/|_| |_|___/
              |_|                                                  
```

Step Functions are a way to orchestrate workflows.

They:
* Visualise your serverless application
* Automatically trigger and track steps (the output of one step is often the input to the next)
* Log the state of each step

The orchestration can:
* follow a sequential workflow (one step triggers one step)
* follow a parallel workflow (one step triggers many steps which can converge to one step)
* follow a branching workflow (one step triggers one step OR a different step based on state)

## Workflows
* ### STANDARD WORKFLOWS
    * **long-running**: durable and auditable, they `run for up to a year`, and once complete, the full history is available for up to 90 days
    * **at-most-once**: `tasks run once`, unless you explicitly specify retry actions
    * **`non-idempotent`**: always causes change in state even with identical requests
* ### EXPRESS WORKFLOWS
    * **short-lived**:  `runs for up to 5 minutes`, ideal for high-volume, event-processing-type workloads
    * **at-least-once**: ideal if you _might_ run an execution more than once, or for `concurrency`
    * **idempotent**: identical requests don't cause side effects
    * **synchronous _or_ asynchronous**:
        * _synchronous_: waits for completion then returns result
        * _asynchronous_: results get left in cloudwatch logs
