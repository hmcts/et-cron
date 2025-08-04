# ET Cron Helm Chart

Helm chart for the ET kubernetes cron job. It uses the [et-cos]([https://github.com/hmcts/et-ccd-callbacks]) image to execute scheduled tasks by passing the arguments: `run [taskname]` to the jar.
