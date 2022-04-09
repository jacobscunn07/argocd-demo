## Quick Start

### Create Cluster
```sh
kind create cluster --config=kind-cluster-config.yaml
```

### Install ArgoCD
```sh
kubectl create ns argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.3.3/manifests/install.yaml
```

Get ArgoCD admin password
```sh
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

Access ArgoCD UI
```sh
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

In a browser, navigate to `http://localhost:8080` and login using the username `admin` and the password from the previous step.

Bootstrapp Applications
```sh
kubectl apply -k ./clusters/overlays/kind-bird
```
