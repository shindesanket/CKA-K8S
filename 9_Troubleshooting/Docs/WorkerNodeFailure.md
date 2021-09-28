
# Worker Node Failures

[Troubleshooting clusters]("https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/")

```bash
kubectl get nodes
```

```bash
ssh key-gen
cd ~/.ssh
cat id_rsa.pub
```

```txt
Click on worker1 on the lab and go to worker node 1
```

```bash
cd ~/.ssh
sudo vi authorized_keys
```

```txt
Paste the content copied from id_rsa.pub and go back to the master node
```

Run below commands on master node

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
