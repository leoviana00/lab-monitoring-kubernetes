## Deployments e ScaleObjects

- Criar namespace `team1`

```bash
kubectl create ns team1
```
- Criar deployments para realização de testes de scalonamento

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