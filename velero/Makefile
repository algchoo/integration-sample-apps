# Start minikube, install velero, install/configure grafana agent, generate load
.PHONY: run
run: 
	minikube start

# Starting minikube
.PHONY: start
start: 
	minikube start

# Installing Velero
.PHONY: install-velero
install-velero:
	# VELERO INSTALL COMMAND
	velero install \
	--provider gcp \
	--bucket prometheus-velero \
	--secret-file /Users/austingeorgiades/Desktop/gcp-api-key-json/upheld-momentum-328313-a741f2b82db2.json \
	--plugins velero/velero-plugin-for-gcp:v1.8.0;

# Load generation
.PHONY: generate-load
generate-load:
	# deploy nginx to a few namespaces
	helm install my-nginx bitnami/nginx --version 15.14.0 --create-namespace --namespace demo-0
	helm install my-nginx bitnami/nginx --version 15.14.0 --create-namespace --namespace demo-1
	# backup those namespaces
	velero backup create demo-0 --include-namespaces demo-0
	velero backup create demo-1 --include-namespaces demo-1
	# delete the namepsaces
	kubectl delete ns demo-0
	kubectl delete ns demo-1
	# restore from backups
	velero create restore --from-backup demo-0
	velero create restore --from-backup demo-1

# Install Grafana Agent
# Configure Grafana Agent

# Teardown
