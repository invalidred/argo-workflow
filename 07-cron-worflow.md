# CronWorkflow

CronWorkflow helps run a workflow at specified schedule.

Note this does not use K8s CRON & JOB. It's a custom Argo implementation.

```bash
Usage:
  argo cron [flags]
  argo cron [command]

Available Commands:
  create      create a cron workflow
  delete      delete a cron workflow
  get         display details about a cron workflow
  lint        validate files or directories of cron workflow manifests
  list        list cron workflows
  resume      resume zero or more cron workflows
  suspend     suspend zero or more cron workflows
```

## Creating a CronWorkflow

```bash
argo cron create 07-cron-workflow.yaml


Name:                          hello-world-nc2ws
Namespace:                     argo
Created:                       Sun Nov 12 14:29:05 -0500 (now)
Schedule:                      */3 * * * *
Suspended:                     false
Timezone:                      America/Los_Angeles
ConcurrencyPolicy:             Replace
NextScheduledTime:             Sun Nov 12 14:30:00 -0500 (54 seconds from now) (assumes workflow-controller is in UTC)
```

## View CronWorkflow

```bash
argo cron list


# output
NAME                AGE   LAST RUN   NEXT RUN   SCHEDULE      TIMEZONE              SUSPENDED
hello-world-nc2ws   3m    2m         30s        */3 * * * *   America/Los_Angeles   false
```

Then you can view workflows run for cron

```bash
argo list -l workflows.argoproj.io/cron-workflow=hello-world-nc2ws
```