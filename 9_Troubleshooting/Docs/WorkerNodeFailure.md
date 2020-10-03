
# Worker Node Failures

[Troubleshooting clusters]("https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/")

```bash
kubectl get nodes
```

```bash
ssh worker-1
```

```bash
ps -ef | grep -i kubelet
```

```bash
systemctl status kubelet.service
```

```bash
systemctl restart kubelet
```

```bash
systemctl status kubelet.service -l
```

```bash
journalctl -u kubelet
```

```bash
cd /etc/systemd/system/kubelet.service.d/
```

