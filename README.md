# example-kustomize-cronjob-multiple-schedule

Example kustomization to generate multiple cronjobs from one common template.

Run:

```
$ kustomize build
```

Expects:

```yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: greeting-midnight
spec:
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - args:
            - It's midnight.
            command:
            - echo
            image: alpine:latest
            name: main
  schedule: 0 0 * * *
---
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: greeting-midnight-monday
spec:
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - args:
            - It's midnight, Monday.
            command:
            - echo
            image: alpine:latest
            name: main
  schedule: 0 0 * * 1
---
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: greeting-morning
spec:
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - args:
            - Good morning.
            command:
            - echo
            image: alpine:latest
            name: main
  schedule: 0 9 * * *
```
