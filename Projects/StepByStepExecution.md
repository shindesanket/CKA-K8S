
# Project execution steps

Pre-requisite :
Install Docker Desktop if you are windows

1). Create Docker Image. Go to the path where DockerFile of the application is present

```bash
docker build -t ckademo .
```

2). Tag the images as per the container registry used ( Following example is for Azure. Please google for AWS and GCP)

```bash
docker tag ckademo myregistry.azurecr.io/mvcapp
```

3). Push the image to the registry

```bash
docker push myregistry.azurecr.io/mvcapp
```

4). Execute kubernetes manifest files in order

```bash
kubectl apply -f mssql-configmap.yaml
kubectl apply -f mssql-pv.azure.yaml
kubectl apply -f mssql-deployment.yaml
kubectl apply -f mvc-deployment.azure.yaml
```
