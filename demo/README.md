# Workshop de Observabilidade
> Tempo estimado: 2 horas

Demo de observabilidade apresentada no workshop.

## Requisitos
Para melhor aproveitamento desse workshop, é esperado que você tenha conhecimentos prévios em:
* Kubernetes
* Docker
* Conceitos de Observabilidade

## Componentes
* Aplicação/Serviço
* OpenTelemetry Collector
* Jaeger UI
* Grafana
* Prometheus
* Loki


## Como Funciona
TBD

## Instalação/Configuração

### Instalação das ferramentas necessárias

Primeiro vamos instalar o kind (para criar clusters k8s localmente usando docker como container runtime):
```bash
# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.24.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

Para interagir com o cluster, vamos instalar o kubectl:
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

E para instalação de aplicações no cluster, vamos usar o Helm:
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

### Configuração do cluster Kubernetes

```bash
kind create cluster --name otel-demo
```
Vai levar alguns minutos para configurar, quanto tiver terminado, pode validar com o comando
```bash
kubectl get node
```

### Configuração da aplicação de demonstração
TBD

### Configuração do Loki(backend para indexar logs)
TBD

### Configuração do Prometheus (backend para exportar métricas)
TBD

### Configuração do Jaeger/Jaeger UI (backend para exportar traces)
TBD

### Configuração do OpenTelemetry Collector (coleta dos sinais)
TBD

### Configuração do Grafana (ferramenta para visualização de logs, métricas e traces)
TBD












