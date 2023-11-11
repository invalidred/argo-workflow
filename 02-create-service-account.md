## Run workflow using custom service account

Create service account and run workflow using that service account

```bash
kubectl create serviceaccount me -n argo

kubectl create rolebinding me \
  --serviceaccount=argo:me \
  --role=executor
```

Then run workflow using the custom sa

```bash
argo submit --serviceaccount me 01-hello-workflow.yaml --watch
```