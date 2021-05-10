# Minio DEMO

To replicate results please fallow these steps:

1. Create cluster and follow Portworx instalation tutorial found here - https://docs.portworx.com/portworx-install-with-kubernetes/cloud

2. Create Namespaces and StorageClass by running `kubectl apply -f RunMeFirst.yaml`

3. Create Minio deployment by running `kubectl apply -f MinioSinglePod.yaml`

4. Deploy two Minio distributed Statefulsets by running commands below:

- Add bitnami repo - `helm repo add bitnami https://charts.bitnami.com/bitnami`

- Install Minio with default storage - `helm install -n minio-dist --set mode=distributed --set accessKey.password=minio --set secretKey.password=minio123 --set service.type=LoadBalancer minio-default-dist bitnami/minio`

- Install Minio with use of Portworx storage - `helm install -n minio-dist-w-repl --set global.storageClass=minio-sc --set mode=distributed --set accessKey.password=minio --set secretKey.password=minio123 --set schedulerName=stork --set service.type=LoadBalancer minio-dist bitnami/minio`