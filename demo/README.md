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

Antes de tudo, faça o clone do repositório:
```bash
git clone git@github.com:cloudnativern/minicurso-encom-o11y.git
```
A partir daqui, todos os comandos devem ser executados a partir do repositório, dentro do diretório `demo/`.   


Para instalar as dependências, executar:
```bash
make setup-deps
```

Após isso, crie o cluster k8s local: 
```bash
make setup-cluster
```

Após o cluster estar executando, faça a instalação da aplicação demo:
```bash
make setup-demo
```











