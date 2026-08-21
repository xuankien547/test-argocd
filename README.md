# test-argocd

This repository archives Kubernetes deploy manifests and a Helm chart repository.

## Repository Structure

```
.
├── deploy/               # Kubernetes manifest files (raw deploy files)
│   ├── deployment.yaml
│   └── service.yaml
├── charts/               # Helm chart source
│   └── myapp/
│       ├── Chart.yaml
│       ├── values.yaml
│       └── templates/
└── helm-repo/            # Helm repository (packaged charts + index)
    ├── index.yaml
    └── myapp-0.1.0.tgz
```

## Deploy Files

The `deploy/` directory contains plain Kubernetes YAML manifests that can be applied directly:

```bash
kubectl apply -f deploy/
```

## Helm Repository

The `helm-repo/` directory serves as a Helm chart repository.

### Add as a Helm repo

```bash
helm repo add test-argocd https://xuankien547.github.io/test-argocd/helm-repo
helm repo update
```

### Install the chart

```bash
helm install myapp test-argocd/myapp
```

### Package and update the repo index (after chart changes)

```bash
helm package charts/myapp -d helm-repo/
helm repo index helm-repo/ --url https://xuankien547.github.io/test-argocd/helm-repo
```