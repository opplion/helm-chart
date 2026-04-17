# Makefile for Helm deployment

RELEASE := blog
NAMESPACE := blog
CHART_DIR := .
PACKAGE_DIR := helm-packages
VALUES_FILE := values.yaml

# Default target
.PHONY: help
help:
	@echo "Makefile commands for Helm:"
	@echo "  make install     - Install Helm chart"
	@echo "  make upgrade     - Upgrade or install Helm release"
	@echo "  make uninstall   - Uninstall Helm release"
	@echo "  make status      - Get Helm release status"
	@echo "  make lint        - Lint Helm chart"
	@echo "  make package     - Package Helm chart into .tgz"

# Install Helm release
.PHONY: install
install:
	@echo "Installing Helm release '$(RELEASE)' in namespace '$(NAMESPACE)'..."
	helm install $(RELEASE) $(CHART_DIR) \
		--namespace $(NAMESPACE) \
		--create-namespace \
		--values $(VALUES_FILE)

# Upgrade Helm release (upgrade or install if not exists)
.PHONY: upgrade
upgrade:
	@echo "Upgrading (or installing) Helm release '$(RELEASE)' in namespace '$(NAMESPACE)'..."
	helm upgrade --install $(RELEASE) $(CHART_DIR) \
		--namespace $(NAMESPACE) \
		--create-namespace \
		--values $(VALUES_FILE) \
		--reuse-values

# Uninstall Helm release
.PHONY: uninstall
uninstall:
	@echo "Uninstalling Helm release '$(RELEASE)' from namespace '$(NAMESPACE)'..."
	helm uninstall $(RELEASE) --namespace $(NAMESPACE)

# Get status of Helm release
.PHONY: status
status:
	@echo "Getting status of Helm release '$(RELEASE)'..."
	helm status $(RELEASE) --namespace $(NAMESPACE)

# Lint Helm chart
.PHONY: lint
lint:
	@echo "Linting Helm chart at $(CHART_DIR)..."
	helm lint $(CHART_DIR)
# Package Helm chart
.PHONY: package
package:
	@echo "Packaging Helm chart from $(CHART_DIR) into $(PACKAGE_DIR)..."
	mkdir -p $(PACKAGE_DIR)
	helm package $(CHART_DIR) --destination $(PACKAGE_DIR)
	@echo "Chart packaged successfully."