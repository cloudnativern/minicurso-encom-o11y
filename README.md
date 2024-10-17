# Workshop de Observabilidade
> Tempo estimado: 2 horas

## Requisitos

Para melhor aproveitamento desse workshop, é esperado que você tenha conhecimento prévio em:
* Kubernetes
* Docker
* Conceitos teóricos de Observabilidade


Ferramentas necessárias para executar a demo:
* Docker
* kind, kubectl e helm são opcionais, podem ser instalados via `Make`


## Componentes

Essa demonstração é usada oficialmente pelo projeto OpenTelemetry, com apenas algumas modificações.   
Abaixo os componentes que fazem parte:

* [Serviços e Dependências (da aplicação)](https://opentelemetry.io/docs/demo/services/)
* [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/)
* [Jaeger UI](https://www.jaegertracing.io/)
* [Locust](https://locust.io/)
* [Grafana](https://grafana.com/oss/grafana/)
* [Prometheus](https://prometheus.io/)
* [OpenSearch](https://opensearch.org/)

## Como Funciona

TL;DR: os sinais emitidos (logs, métricas e traces) pelos componentes da aplicação são coletados e processados pelo OTel Collector e enviados para os backends:

* Prometheus para métricas
* Jaeger para traces
* Opensearch para logs

E todos esses backends estão configurados para visualização no Grafana.

Diagrama de arquitetura completa: https://opentelemetry.io/docs/demo/architecture/

## Instalação/Configuração

Antes de tudo, faça o clone do repositório:

```bash
git clone git@github.com:cloudnativern/o11y-workshop.git
```

**A partir daqui, todos os comandos devem ser executados a partir do repositório, dentro do diretório `demo/`.**   


#### 1. Instale as dependências:
> Se você já tiver as dependências instaladas (kind, helm e kubectl), pode pular essa etapa 

```bash
make setup-deps
```

#### 2. Após isso, crie o cluster k8s local: 

```bash
make setup-cluster
```

#### 3. Após o cluster estar executando, faça a instalação da aplicação demo:

```bash
make setup-demo
```

A aplicação vai levar em torno de 8-10 minutos para estar pronta, para checar se todos os *Pods* estão executando corretamente:
```bash
kubectl get po -n otel-demo
```

#### 4. Após estar executando corretamente, exponha o proxy que vai permitir que seja feito o acesso aos componentes da demonstração (na porta `8080`):
```bash
make expose-demo
```

Sendo:
* `http://localhost:8080/`: Página inicial da aplicação
* `http://localhost:8080/grafana/`: Grafana
* `http://localhost:8080/loadgen/`: Locust UI
* `http://localhost:8080/jaeger/ui/`: Jaeger UI


Se quiser/precisar fazer alguma alterações nas configurações da demo (`demo/values.yaml`), execute o comando abaixo para atualizar:
```bash
make upgrade-demo
```

## Cleanup
Ao final, do workshop, executar o comando abaixo para remover todos os recursos:
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








