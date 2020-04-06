# Helm Chart for Apache Flink with MinIO
Helm chart to deploy a [Flink](https://flink.apache.org/) cluster as well as a [MinIO](https://min.io/) (S3 Object Storage) instance. This can be used for local development and testing of Flinks checkpointing mechanism backed up by S3 storage.

# Prereqs
## Dockerfile
Build a local image with linked Presto S3 dependencies.
```
$ docker build -t flink-custom:1.10.0-scala_2.12-1 docker/
```

# Usage
## Helm
### Install dependencies
```
$ helm install sunny stable/minio --namespace <NAMESPACE> -f minio-values.yaml
```

### Create
```
$ helm install --namespace <NAMESPACE> <NAME> flink/
```

### Upgrade
```
$ helm upgrade --namespace <NAMESPACE> <NAME> flink/
```

### Delete
```
$ helm delete --namespace <NAMESPACE> <NAME>
```

## Web access
### MinIO
Port-forward to localhost:
```
$ kubectl port-forward $(kubectl get pods --namespace <NAMESPACE> -l "release=<NAME>" -o jsonpath="{.items[0].metadata.name}") 9000 --namespace <NAMESPACE>
```
Access: http://localhost:9000

### Flink WebUI
Port-forward to localhost:
```
$ kubectl port-forward $(kubectl get pods --namespace <NAMESPACE> -l "release=<NAME>" -l "component=jobmanager" -o jsonpath="{.items[0].metadata.name}") 8081 --namespace <NAMESPACE>
```
Access: http://localhost:8081

