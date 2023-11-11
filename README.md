# Argo workflows

## Prerequsites
- Docker desktop
- [kubens](https://webinstall.dev/kubens/): enables sticking to namespace `kubens argo`

## Setup

This project leverages [k3d](https://k3d.io/v5.6.0/)

_To create a local kubernetes cluster_
```bash
# Ensure you've got Docker Desktop installed
# Install k3d
brew install k3d

# Install cluster
k3d cluster create k3s-default --agents 3 [--servers 3]
k3d kubeconfig write k3s-default

# Verify cluster is created and connected
kubectl cluster-info
```

_Other useful k3d commands_
```bash
k3d cluster list
k3d cluster stop k3s-default
k3d cluster start k3s-default
k3s cluster delete k3s-default
```

## Install argo workflow
```bash
brew install argo
argo version
```

_complete setting up argo workflow components_

```bash
kubectl create ns argo
kubectl -n argo apply -f ./quick-start-postgres.yaml

# takes maybe 2m for all pods to be ready
kubectl -n argo get pods --watch

kubectl -n argo port-forward svc/argo-server 2746:2746
open http://localhost:2746
```
