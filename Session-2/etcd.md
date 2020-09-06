# ETCD

## Working with etcd

---

### Distributed key value store

1. Download the etcd by using the below command -

```bash
ETCD_VERSION=3.4.10
wget https://github.com/etcd-io/etcd/releases/download/v${ETCD_VERSION}/etcd-v${ETCD_VERSION}-linux-amd64.tar.gz
```
2. Unzip the compressed binaries
 
```bash
tar xvf etcd-v${ETCD_VERSION}-linux-amd64.tar.gz
```

3. Move the files into the `/usr/local/bin` using command -

```bash
sudo mv etcd-v${ETCD_VERSION}-linux-amd64/etcd* /usr/bin
```

4. View the page for etcdctl help using command -

```bash
ETCDCTL_API=3 etcdctl --help
```

5. To view all the keys from the etcd distributed data store use the command -

```bash
sudo ETCDCTL_API=3 etcdctl get / --prefix --keys-only \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
--cacert=/etc/kubernetes/pki/etcd/ca.crt
```

6. To add a new key to the etcd distributed data store use the command -

```bash
sudo ETCDCTL_API=3 etcdctl put firstname sanket \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
--cacert=/etc/kubernetes/pki/etcd/ca.crt
```

7. To get a value of key from the etcd distributed data store use the command -

```bash
sudo ETCDCTL_API=3 etcdctl get firstname \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
--cacert=/etc/kubernetes/pki/etcd/ca.crt
```

8. To delete the key from the etcd distributed data store use the command -

```bash
sudo ETCDCTL_API=3 etcdctl del firstname \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
--cacert=/etc/kubernetes/pki/etcd/ca.crt
```

---

