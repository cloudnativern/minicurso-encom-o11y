# Workshop de Observabilidade
> Tempo estimado: 2 horas

Demo de observabilidade apresentada no workshop.

## Requisitos
Para melhor aproveitamento desse workshop, é esperado que você tenha conhecimentos prévios em:
* Kubernetes
* Docker
* Conceitos teóricos de Observabilidade

## Componentes

Essa demo, é a mesma usada oficialmente pelo projeto OpenTelemetry, apenas com algumas modificações.   
Abaixo os componentes que fazem parte:

* [Serviços e dependências (da aplicação)](https://opentelemetry.io/docs/demo/services/)
* OpenTelemetry Collector
* Jaeger UI
* Locust
* Grafana
* Prometheus

## Como Funciona

TL;DR: os sinais emitidos (logs, métricas e traces) pelos componentes da aplicação são coletados e processados pelo OTel Collector e enviados para os backends:

* prometheus para métricas
* jaeger para traces
* opensearch para logs

E todos esses backends estão configurados para visualização no Grafana.

Diagrama de arquitetura completa: https://opentelemetry.io/docs/demo/architecture/

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
A aplicação vai levar em torno de 5-8 minutos para estar pronta, para checar se todos os *Pods* estão executando corretamente:
```bash
kubectl get po -n otel-demo
```

Após estar executando corretamente, exponha o proxy que vai permitir que seja feito o acesso aos componentes da demonstração (na porta `8080`):
```bash
make expose-demo
```

Sendo:
* `http://localhost:8080/`: aplicação
* `http://localhost:8080/grafana/`: Grafana
* `http://localhost:8080/loadgen/`: Locust UI
* `http://localhost:8080/jaeger/ui/`: Jaeger UI


Ao final, quando terminar o workshop, executar o comando abaixo para remover todos os recursos:
```bash
make cleanup
```

## Referências e outras sugestões
* https://opentelemetry.io/docs/demo/
* https://dosedetelemetria.com/
* Outras recomendações de ferramentas opensource para Observabilidade:
    * Grafana Tempo: backend para traces
    * Grafana Mimir: backend para métricas
    * Grafana Loki: backend para logs








