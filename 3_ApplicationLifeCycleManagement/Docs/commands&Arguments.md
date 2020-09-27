# Commands & Arguments

[K8s Documentation for Commands & Arguements](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/)

## commands.yaml

```yml
apiVersion: v1
kind: Pod
metadata:
  name: command-demo
  labels:
    purpose: demonstrate-command
spec:
  containers:
  - name: command-demo-container
    image: debian
    command: ["printenv"]
    args: ["HOSTNAME", "KUBERNETES_PORT"]
  restartPolicy: OnFailure
```

```bash
kubectl apply -f commands.yaml
```

```bash
kubectl get pods
```

```bash
kubectl logs command-demo
```

## Run a command in a shell

### commands-shell.yaml

```yml
apiVersion: v1
kind: Pod
metadata:
  name: command-demo
  labels:
    purpose: demonstrate-command
spec:
  containers:
  - name: command-demo-container
    image: debian
    command: ["/bin/sh"]
    args: ["-c", "while true; do echo hello; sleep 10;done"]
  restartPolicy: OnFailure
```

```bash
kubectl apply -f commands-shell.yaml
```

```bash
kubectl get pods
```

```bash
kubectl logs command-demo
```
