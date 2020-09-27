# Installing Metrics Server

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.3.7/components.yaml
```

Once deployed edit the deployment by using the command -

```bash
kubectl edit -n kube-system deploy/metrics-server
```

In the spec section of pod template, add a command specification as shown below -

```yml
  command:
  - /metrics-server
  - --kubelet-insecure-tls=true
  - --kubelet-preferred-address-types=InternalIP
```

Wait for the deployment to be updated.

```bash
kubectl top pod
kubectl top pod --namespace=<namespace_name>
kubectl top pod <pod_name> --containers
kubectl top node
kubectl top node <node_name> # Gets individual node CPU and Memory usage
```

[Reference Link](https://github.com/kubernetes-sigs/metrics-server)
