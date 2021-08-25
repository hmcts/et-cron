# NFDIV Cron Helm Chart

Helm chart for the NFDIV kubernetes cron job. It uses the [nfdiv-case-api](https://www.github.com/hmcts/nfdiv-case-api) image to execute scheduled tasks by passing the arguments: `run [taskname]` to the jar.
