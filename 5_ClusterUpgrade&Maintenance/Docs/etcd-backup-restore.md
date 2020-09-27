# ETCD Backup and Restore

## Install ETCD

```txt
1. Download the etcd by using the below command -
```

```bash
ETCD_VERSION=3.4.10
wget https://github.com/etcd-io/etcd/releases/download/v${ETCD_VERSION}/etcd-v${ETCD_VERSION}-linux-amd64.tar.gz
```

```txt
2. Unzip the compressed binaries
```

```bash
tar xvf etcd-v${ETCD_VERSION}-linux-amd64.tar.gz
```

```txt
3. Move the files into the `/usr/local/bin` using command -
```

```bash
sudo mv etcd-v${ETCD_VERSION}-linux-amd64/etcd* /usr/local/bin
```

```txt
4. View the page for etcdctl help using command -
```

```bash
ETCDCTL_API=3 etcdctl --help
```

```txt
5. To view all the keys from the etcd distributed data store use the command -
```

```bash
sudo ETCDCTL_API=3 etcdctl get / --prefix --keys-only \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
--cacert=/etc/kubernetes/pki/etcd/ca.crt
```

```txt
6. As ETCD is successfully installed, please create nginx and redis deployments using following commands
```

```bash
kubectl create deployment nginx --image nginx
kubectl create deployment redis --image redis
kubctl scale deployment nginx --replicas 6
kubectl scale deployment redis --replicas 6
```

```txt
7. Describe the ETCD pod running in kube-system namespace. Observe --cacert, --cert, --key, --endpoints
```

```bash
kubectl describe pod "ETCD pod Name" -n kube-system
```

```txt
8. Check all options of ETCD Snapshot save command
```

```bash
sudo ETCDCTL_API=3 etcdctl snapshot save -h
```

```txt
9. Check if you have copied correct --cacert, --cert, --key, --endpoints by following command
```

```bash
sudo ETCDCTL_API=3 etcdctl member list --cacert=/etc/kubernetes/pki/etcd/ca.crt --cert=/etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key --endpoints=127.0.0.1:2379
```

```txt
10. Command to save the Snapshot of ETCD.
```

```bash
sudo ETCDCTL_API=3 etcdctl snapshot save --cacert=/etc/kubernetes/pki/etcd/ca.crt --cert=/etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key --endpoints=127.0.0.1:2379 snapshot-etcd.db
```

```txt
11. Check if snapshot-etcd.db generated on the current directory
```

```txt
12. Delete all the deployments and pods from the system
```

```bash
kubectl delete all --all
```

```txt
13. Check all options of ETCD Restore command
```

```bash
sudo ETCDCTL_API=3 etcdctl snapshot restore -h
```

```txt
14. Command to save the Snapshot of ETCD.
```

```bash
sudo ETCDCTL_API=3 etcdctl snapshot restore --cacert=/etc/kubernetes/pki/etcd/ca.crt --cert=/etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key --endpoints=127.0.0.1:2379 --data-dir="/var/lib/etcd-from-backup" --initial-cluster="Master Node Name=https://127.0.0.1:2380" --name="Master Node Name" --initial-advertise-peer-urls="https://127.0.0.1:2380" --initial-cluster-token="etcd-cluster-1" snapshot-etcd.db
```

```txt
15. Go to "/var/lib/etcd-from-backup" and check if member folder is present
```

```txt
16. Go to ETCD static pod configuration at etc/kuberenetes/manifest and Update following values
Update : - --data-dir=/var/lib/etcd-from-backup
Add :  - --initial-cluster-token="etcd-cluster-1"
Update : volumeMounts:
         - mountPath: /var/lib/etcd-from-backup
Update : - hostPath:
         path: /var/lib/etcd-from-backup
```

```bash
sudo vi etcd.yaml
```

```txt
17. Watch docker ps command to check if etcd pod is restarted.
```

```bash
watch "docker ps"
```

```txt
18. Check if nginx and redis deployments are restored
```

```bash
kubectl get all
```
