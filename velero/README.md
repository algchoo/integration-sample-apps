### Velero on Minikube with GCP Bucket
---
#### Prerequisites
* Install the [velero cli](https://velero.io/docs/v1.9/basic-install/)
* Access to a Google Cloud Platform project
    * Permission to create a service account
    * Permission to create a storage bucket
* Create a service account (Owner permissions are fine for a ***dev*** project, see VMWare docs for an LPU) and download its json key.
* Create a storage bucket with the default parameters and the name `prometheus-velero`.

#### Install

Deploy Velero to `velero` namespace, where `<PATH_TO_JSON_FILE>` points to the service account json key file.

```bash
velero install \
  --provider gcp \
  --bucket prometheus-velero \
  --secret-file <PATH_TO_JSON_KEY_FILE> \
  --plugins velero/velero-plugin-for-gcp:v1.8.0
```

#### Loadgen

<!-- Update this section based after building makefile -->
Create backups, where `default` is the name of the backup for namespace `default`.


```bash
velero backup create default --include-namespaces default
velero backup create invalid --include-namespaces invalid
```

#### Documentation
* [GCP Plugin Repository](https://github.com/vmware-tanzu/velero-plugin-for-gcp)
