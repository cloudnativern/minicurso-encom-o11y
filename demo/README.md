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
* `http://localhost:8080/loadgen/`: Load Generator UI
* `http://localhost:8080/jaeger/ui/`: Jaeger UI


Ao final, quando terminar o workshop, executar o comando abaixo para remover todos os recursos:
```bash
make cleanup
```









