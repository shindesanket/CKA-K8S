# Commands to troubleshoot Application Failure

1). Check frontend service for endpoints and selectors

```bash
kubectl describe service <service name>
```

2). If no issue found in fronend service, check front end pod

```bash
kubectl get pods
kubectl describe pod <pod name>
```

3). Check logs of a pod

```bash
kubectl logs <pod name>
```

4). Check for backend and db services and pods using same commands.
