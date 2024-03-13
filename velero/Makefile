# Start minikube, install velero, install/configure grafana agent, generate load
.PHONY: run
run: minikube start

# Starting minikube
.PHONY: start-minikube
start-minikube: minikube start

# Installing Velero
.PHONY: install-velero
install-velero:
	# VELERO INSTALL COMMAND
	velero install \
	--provider gcp \
	--bucket prometheus-velero \
	--secret-file $GCP_SERVICE_ACCOUNT_JSON_KEY \
	--plugins velero/velero-plugin-for-gcp:v1.8.0
	
# Install Grafana Agent

# Configure Grafana Agent
# Load generation
# Teardown
