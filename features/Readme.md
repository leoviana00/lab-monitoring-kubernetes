## Instalação de algumas features kubernetes utilizando o kustomize e argocd

- Cert Manager
- Cluster Issuer
- Metrics Server
- Nginx Ingress
- Kube Stak Prometheus

## Instalação do argo-cd

```bash
helm repo add argocd https://argoproj.github.io/argo-helm
helm repo update
kubectl create ns argo-cd
helm install -name argocd argocd/argo-cd -f values.yaml -n argo-cd
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```