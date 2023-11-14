## Monitoring Kubernetes Stack

## Ferramentas

- Grafana
- Prometheus
- AlertManager
- Loki
- Ptomtail

## Instalação

- Step 1: Adicionar repositórios Helm

```bash
helm repo add kedacore https://kedacore.github.io/charts
helm repo add argo https://argoproj.github.io/argo-helm
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update 
```

```console
Kube-Prometheus-stack, também como Operador Prometheus, é um projeto popular de código aberto que fornece soluções completas de monitoramento e alerta para clusters Kubernetes. Ele combina ferramentas e componentes para criar uma pilha de monitoramento para ambientes Kubernetes.
```

- Step 2: Criar namespace `monitoring`

```bash
kubectl create ns monitoring
```

- Step 3: Instalar `Kube-Prometheus-stack`

```console
Usará o Helm Chart Kube-Prometheus-stack oficial,
com um arquivo de valor customizado.
```

```bash
helm upgrade --install -f prometheus-stack/values.yaml kube-prometheus-stack prometheus-community/kube-prometheus-stack -n monitoring
```

- Step 3.1: Instalar Service Monitor

```bash
kubectl apply -f prometheus-stack/servicemonitor.yaml -n monitoring
```

- Step 4: Instalar o Loki

```bash
helm upgrade --install -f loki/loki-distributed.yaml loki grafana/loki-distributed -n monitoring
```

- Step 5: Install Ptomtail

```bash
helm upgrade --install -f promtail/promtail.yaml promtail grafana/promtail -n monitoring
```

## Dashboard Grafana

- https://grafana.com/grafana/dashboards/14055-loki-stack-monitoring-promtail-loki/ 
- https://grafana.com/grafana/dashboards/16966-container-log-dashboard/ 