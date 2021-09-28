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

3) Go to etc/kubernetes/manifest and open yaml file of control plane components

```bash
sudo cat <<yaml file>>
```

4) Steps to troubleshoot control plane components

```txt
1) Check the logs for that control plane pod

2) Go to ect/kubernetes/manifest and open yaml manifest for respective yaml

3) Check for certificates and ports
```


