
.PHONY: help
help: ## this help
	@awk 'BEGIN {FS = ":.*##"; printf "\nUsage:\n  \033[36m\033[0m\n"} /^[$$()% a-zA-Z_-]+:.*?##/ { printf "  \033[36m%-15s\033[0m %s\n", $$1, $$2 } /^##@/ { printf "\n\033[1m%s\033[0m\n", substr($$0, 5) } ' $(MAKEFILE_LIST)

.PHONY: setup-deps
setup-deps: ## install dependencies
		@echo "Installing dependencies...."
		@command -v kind >/dev/null 2>&1 || { echo >&2 "kind is not installed, installing..."; curl -Lo ./kind-bin https://kind.sigs.k8s.io/dl/v0.24.0/kind-linux-amd64; sudo chmod +x ./kind-bin; sudo mv ./kind-bin /usr/local/bin/kind; }
		@echo "Kind installed!"
		@command -v kubectl >/dev/null 2>&1 || { echo >&2 "kubectl is not installed, installing..."; curl -LO https://dl.k8s.io/release/v1.31.0/bin/linux/amd64/kubectl; sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl; rm kubectl;}
		@echo "Kubectl installed!"
		@command -v helm >/dev/null 2>&1 || { echo >&2 "helm is not installed, installing..."; curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3; chmod 700 get_helm.sh; ./get_helm.sh; rm get_helm.sh;  }
		@echo "Helm installed!"
		@echo "\n"
     
.PHONY: setup-cluster
setup-cluster: ## setup kind cluster
		@echo "Creating kind cluster"
		kind create cluster --config kind/cfg-cluster.yaml

.PHONY: setup-demo
setup-demo: ## setup demo application
		@echo "Setting up the demo app"
		helm repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts
		helm install --create-namespace otel-demo open-telemetry/opentelemetry-demo -f values.yaml -n otel-demo

.PHONY: update-demo
update-demo: ## update demo values
	@echo "Updating the demo app"
	helm upgrade otel-demo open-telemetry/opentelemetry-demo -f values.yaml -n otel-demo


.PHONY: expose-demo
expose-demo: ## expose the port to access the demo
	@echo "Setting up the demo app"
	kubectl port-forward svc/otel-demo-frontendproxy 8080:8080 -n otel-demo

.PHONY:cleanup
cleanup: ## cleanup environment
		@echo "Cleaning up the resources"
		helm uninstall otel-demo -n otel-demo
		kind delete cluster --name otel-demo


