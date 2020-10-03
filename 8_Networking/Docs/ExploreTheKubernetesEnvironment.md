# Explore the Kubernetes Networking

1). How many nodes are part of the cluster?

```bash
kubectl get nodes
```

2). What is the network interface configured for cluster connectivity on the master network?

```bash
ip link
```

3). What is the IP address assigned to master node on this interface?

```bash
ifconfig eth0
ip addr
```

4). What is the MAC address of the inteface on Master node.

```bash
ifconfig eth0
ip link
```

5). What is the ipaddress of default gateway?

```bash
ip r
```

6). What is the port KubeScheduler is listening on master node?

```bash
netstat -natulp | grep kube-scheduler
```
