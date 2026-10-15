# webapp-gitops

GitOps repository for the WebApp stack (FastAPI + MySQL). **Argo CD** watches this repository and keeps the cluster in sync with it.

```
webapp-gitops/
├── charts/webapp-stack/          Helm chart (templates + default values)
├── environments/dev/values.yaml  values for the dev environment
└── argocd/application.yaml       Argo CD Application that deploys the chart
```

## How to change the deployment

1. Edit `environments/dev/values.yaml` (replicas, image tags, storage size).
2. Commit and push to `main`.
3. Argo CD syncs the change automatically (or click **Refresh** in the UI).

Never change the cluster with `kubectl` directly: Argo CD reverts manual changes (self-heal).

## Bootstrap (once)

```bash
kubectl apply -f argocd/application.yaml
```
