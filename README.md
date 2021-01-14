# <img src="docs/img/hive_helm.png" width="10%"> | HMS Helm Chart 

In simple terms, [Helm](https://helm.sh/) is a package manager for Kubernetes. This Hive chart (package) encapsulates all configurations and components needed to deploy a Hive Metastore service in a Kubernetes cluster.

## Kubernetes Resources used in this Hive Chart

The resources used in the this chart are defined in yaml files inside [`/templates` directory](https://github.com/amommendes/helm-hive-metastore/tree/main/templates). The following resources are used:

- [Configmap](https://github.com/amommendes/helm-hive-metastore/blob/main/templates/configmap.yaml): this kube resource creates volumes that can be attached to containers. Here, we're mounting a volume to the [HMS configuration templates directory](https://github.com/amommendes/helm-hive-metastore/blob/main/templates/deployment.yaml#L65), which will be used by the HMS docker image to render the `metastore-site.yaml` config file.
- [Service](https://github.com/amommendes/helm-hive-metastore/blob/main/templates/service.yaml): this resources is responsible to expose the HMS service to the external.
- Horizontal Pods Autoscaler ([HPA](https://github.com/amommendes/helm-hive-metastore/blob/main/templates/hpa.yaml)): this resource increases the number of pods available in a ReplicaSet based on some thresholds (memory and cpu) in order to guarantee the service availability
- [Deployment](https://github.com/amommendes/helm-hive-metastore/blob/main/templates/deployment.yaml): this the main resource here, because it specifies pod's configurations and is the link between all resources and the HMS pods.
