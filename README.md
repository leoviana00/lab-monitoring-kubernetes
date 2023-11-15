<h1 align="center">Monitoring and Logging</h1>

<p align="center">
  <img alt="Kubernetes" src="https://img.shields.io/static/v1?label=Kubernetes&message=Monitoring&color=8257E5&labelColor=000000"  />
  <img alt="License" src="https://img.shields.io/static/v1?label=license&message=MIT&color=49AA26&labelColor=000000">
</p>

<p align="center">
  <a href="#-projeto">Projeto</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-tecnologias">Tecnologias</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-roadmap">Roadmap</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-referências">Referências</a>
</p>

<p align="center">
  <img alt="Monitoring" src="data/monitoring.png">
</p>

## 💡 Projeto
- Laboratório para testes utilizando uma stack de monitoramento e logs. Realização de testes de autoscaling de aplicações utilizando o hpa e keda.

## ✨ Tecnologias
- Monitoring
    - Grafana
    - Prometheus
    - AlertManager
- Logging
    - Loki
    - Ptomtail
- Autoscaling
    - HPA
    - Keda
    - Metrics
- Kubernetes

## 👣 Roadmap

- [x] [Preparação de um Cluster Kubernetes utilizando o kubespray](/setup/setup-k8s-kubespray/kubespray/kubespray.md)
- [x] [Instalação do Helm](/helm/Readme.md)
- [x] [Instalação da stack de monitoramento](/monitoring/prometheus-stack/Readme.md)
- [x] [Instalação da stack logging](/logging/Readme.md)
- [x] [Instalação do Metrics Server](/monitoring/metrics-server/Readme.md)
- [x] [Instalação do Keda](/autoscaling/keda/Readme.md)
- [x] [Criar aplicações para realização de testes de escalonamento baseado em consumo de memória](/autoscaling/app/Readme.md)
- [x] Integração do grafana com o Prometheus
- [x] Integração do grafana com Loki;
- [x] [Criar Dashboard no grafana para visualização de logs](/dashboards/Readme.md)

## 📄 Referências

- https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/

- https://kubernetes.io/docs/tasks/configure-pod-container/resize-container-resources/