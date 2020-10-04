# Troubleshooting ControlPlane failure

1). Check node status

```bash
kubectl get nodes
```

2). Check status of control plane components in kube-system namespace

```bash
kubectl logs <apiserver pod name> -n kube-system
kubectl logs <etcd pod name> -n kube-system
kubectl logs <controller pod name> -n kube-system
kubectl logs <scheduler pod name> -n kube-system
```

```bash
sudo journalctl -u <controle plane pod name>
```
