# Steps to deploy this project on kubernetes cluster

1) Build a Docker Image using given dockerfile in MvcApp folder.
2) Push this Docker image to your repository on DockerHub
3) Connect to the Kubernetes cluster using kubectl (get-credentials command of respective public cloud providers)
4) Execute YAML manifest file present in kubernetes folder
5) Run command :

```bash
kubectl get all
```
