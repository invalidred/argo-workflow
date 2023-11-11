# Workflow template

```bash

# To create a template
argo template create 06-workflow-template.yaml

# To view template
argo template list
argo template get add-example-template
```

## To refer template in workflow

Use `workflowTemplateRef` as seen below

```yaml
---
apiVersion: argoproj.io/v1alpha1
kind: Workflow
metadata:
  generateName: add-example-
spec:
  workflowTemplateRef:
    name: add-example-template
```

Submit via

```bash
argo submit 06-workflow-template-ref.yaml --watch

# verify using logs
argo logs @latest
```

## To refer only a step in a template

Use `templateRef` as seen below

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Workflow
metadata:
  generateName: workflow-template-hello-world-
spec:
  entrypoint: whalesay
  templates:
    - name: whalesay
      steps:
        - - name: call-whalesay-template
            templateRef:
              name: add-example-template
              template: addfour
            arguments:
              parameters:
                - name: a
                  value: "3"

```

Submit via

```bash
argo submit 06-workflow-partial-template-ref.yaml --watch

# verify using logs
argo logs @latest
```