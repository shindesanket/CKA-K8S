# Deployment Updates and RollBacks

## Create a Deployment using YAML

### Name of file : deployment.yaml

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

### Command to create a deployment

```bash
kubectl apply -f deployment.yaml
```

### This command is to list all deployments

```bash
kubectl get deployments
```

### Other Commands : These commands are used to perform rolling upgrades

```bash
Kubectl apply -f deployment.yaml
```

```bash
kubectl rollout status deployment deployment.yaml
```

```bash
kubectl rollout history deployment deployment.yaml
```

```bash
kubectl set image deployment nginx-deployment nginx=nginx:1.9.1
```

```bash
kubectl rollout undo deployment nginx-deployment
```

```bash
kubectl rollout undo deployment nginx-deployment --to-revision=2
```
