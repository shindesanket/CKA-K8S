# Getting logs of a application

## Create a pod with following manifest

```bash
apiVersion: v1
kind: Pod
metadata:
  name: event-simulator-pod
spec:
  containers:
  - name: event-simulator
    image: kodekloud/event-simulator
```

## Command to see the logs

```bash
kubectl logs -f event-simulator-pod
```

## Command for checking logs of single container in multi container environment

```bash
kubectl logs –f event-simulator-pod event-simulator
```

```txt
We just added container name after the pod name
```