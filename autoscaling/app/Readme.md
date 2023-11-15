## Deployments e ScaleObjects

- Criar namespace `team1`

```bash
kubectl create ns team1
```
- Criar deployments para realização de testes de escalonamento

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: app1-team1
  name: app1-team1
  namespace: team1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: app1-team1
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: app1-team1
    spec:
      containers:
      - image: polinux/stress
        name: stress
        resources:
          requests:
            memory: "100Mi"
          limits:
            memory: "300Mi"
        command: ["stress"]
        args: ["--vm", "1", "--vm-bytes", "200M", "--vm-hang", "1"]
        # args: ["--vm", "1", "--vm-bytes", "290M", "--vm-hang", "1"]
status: {}
```

- Alterar o valor `200M` de acordo com a necessidade para gerar um consumo maior ou menor possibilitando os testes de scaling.

- Criar o ScaledObject

```bash
apiVersion: keda.sh/v1alpha1
kind: ScaledObject
metadata:
  name: app1-team1
  namespace: team1
spec:
  cooldownPeriod: 30
  maxReplicaCount: 4
  minReplicaCount: 1
  pollingInterval: 30
  scaleTargetRef:
    name: app1-team1
  triggers:
  - type: prometheus
    metadata:
      metricName: max-mem-app1-team1
      query: |
        sum(
          container_memory_usage_bytes{
            container!="", 
            pod=~"^app1-team1-.*", 
            namespace="team1"
          }
        ) / 
        sum(
          kube_pod_container_resource_limits{
            resource="memory", 
            pod=~"^app1-team1-.*",
            container!=""
          }
        ) * 100.0
      serverAddress: http://prometheus-operated.monitoring.svc.cluster.local:9090
      threshold: '70'
```

- Consulta usada no `ScaledObject`: Métrica personalizada de limites de uso de memória:

```bash
sum(container_memory_usage_bytes{container!="", pod=~"^app1-team1-.*", namespace="team1"}) / sum(kube_pod_container_resource_limits{resource="memory", container!="", pod=~"^app1-team1-.*"}) * 100.0
```