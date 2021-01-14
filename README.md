# <img src="docs/img/hive_helm.png" width="10%"> | HMS Helm Chart 

In simple terms, [Helm](https://helm.sh/) is a package manager for Kubernetes. This Hive chart (package) encapsulates all configurations and components needed to deploy a Hive Metastore service in a Kubernetes cluster.

## Kubernetes Resources used in this Hive Chart

The resources used in the chart are defined in yaml files inside [`/templates` directory](https://github.com/amommendes/helm-hive-metastore/tree/main/templates). For our HMS chart will use the following resources:

- [Configmap](https://github.com/amommendes/helm-hive-metastore/blob/templates/configmap.yaml): this kube resource creates volumes that can be attached to containers. Here, we're mounting a volume to the [HMS configuration templates directory](https://github.com/amommendes/helm-hive-metastore/blob/27187a6f44a3ea10705cf2df039456ab916e16fc/templates/deployment.yaml#L65), which will be used by the HMS docker image to render the `metastore-site.yaml` config file.
- [Service](https://github.com/amommendes/helm-hive-metastore/blob/templates/service.yaml) and [ServiceAccount](https://github.com/amommendes/helm-hive-metastore/blob/templates/serviceaccount.yaml): these resources are responsible to expose the HMS service to the external world and create account to the pod processes [authentication](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/) in the Kube API.
- Horizontal Pods Autoscaler ([HPA](https://github.com/amommendes/helm-hive-metastore/blob/templates/hpa.yaml)): this resource increases the number of pods available in a ReplicaSet based on some thresholds (memory and cpu) in order to guarantee the service availability
- [Deployment](https://github.com/amommendes/helm-hive-metastore/blob/templates/deployment.yaml): this the main resource here, because it specifies pod's configurations and is the link between all resources and the HMS pods.
