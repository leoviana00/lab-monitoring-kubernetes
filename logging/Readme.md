## Instalação Loki

- Step 1: Adicionar repositórios Helm

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update 
```

- Step 2: Instalar o Loki

```bash
helm upgrade --install -f logging/loki/loki-distributed.yaml loki grafana/loki-distributed -n monitoring
```

- Step 3: Install Ptomtail

```bash
helm upgrade --install -f logging/promtail/values.yaml promtail grafana/promtail -n monitoring
```

