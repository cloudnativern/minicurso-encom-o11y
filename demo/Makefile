
.PHONY: help
help: ## this help
	@awk 'BEGIN {FS = ":.*##"; printf "\nUsage:\n  make \033[36m\033[0m\n"} /^[$$()% a-zA-Z_-]+:.*?##/ { printf "  \033[36m%-15s\033[0m %s\n", $$1, $$2 } /^##@/ { printf "\n\033[1m%s\033[0m\n", substr($$0, 5) } ' $(MAKEFILE_LIST)

.PHONY: setup-deps
setup-deps: ## install dependencies
		@echo "Installing dependencies...."
		@command -v kind >/dev/null 2>&1 || { echo >&2 "kubectl is not installed, installing..."; curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.24.0/kind-linux-amd64; chmod +x ./kind; sudo mv ./kind /usr/local/bin/kind; }
		@echo "Kind installed!"
		@command -v kubectl >/dev/null 2>&1 || { echo >&2 "kubectl is not installed, installing..."; curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"; sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl; }
		@echo "Kubectl installed!"
		@command -v helm >/dev/null 2>&1 || { echo >&2 "helm is not installed, installing..."; curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3; chmod 700 get_helm.sh; ./get_helm.sh; rm get_helm.sh;  }
		@echo "Helm installed!"
		@echo "\n"
     
.PHONY: setup-cluster
setup-cluster: ## setup kind cluster
		@echo "Creating kind cluster"
		kind create cluster --name otel-demo

.PHONY: setup-demo
setup-demo: ## wip:setup demo application
		@echo "Setting up the demo app"

.PHONY:cleanup
cleanup: ## cleanup environment
		@echo "Cleaning up the resources"
		kind delete cluster --name otel-demo


