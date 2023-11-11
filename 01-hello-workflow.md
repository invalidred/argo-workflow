# Hello Worflow

_via ci_
```bash
argo submit hello-workflow.yaml --watch -n argo
```

Not you can also use the argo workflow UI to run workflows.

_Another example_
```bash
argo submit -n argo https://raw.githubusercontent.com/argoproj/argo/master/examples/hello-world.yaml

argo list -n argo
argo get -n argo <workflow-id>
argo logs -n argo <workflow-id>
```