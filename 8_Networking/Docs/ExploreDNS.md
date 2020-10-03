# Explore DNS in Kubeadm setup

1). Identify the DNS solution implemented in the cluster

```bash
kubectl get deployments -n kube-system
```

2). How many pods of DNS server are deployed?

3). What is the name of the service created for accessing CoreDNS?

```bash
kubectl get svc -n kube-system
```

4). What is the ip of the CoreDNS server that should be configured on Pods to resolve services?

5). Where is the configuration file located for configuring DNS service?

```bash
kubectl describe deployments coredns -n kube-system
```

6). How this configuration in passed to coredns server?

7). What is the root domain/zone configured for this cluster?

```bash
kubectl describe cm coredns -n kube-system
```

8). Create 2 new pods called app1 and app2 using image nginx. create a service exposes pod app2 called as app2-service. create new namespace called as demo and add pod app3 to it using image redis expose the pod3 using service called as app3-service.

9). What name can be used to access app2 webserver by app1 pod?

10). Which of the following names cannot be used to access the app2 from app1?

```txt
1) app2-service.default.svc
2) app2-service.default
3) app2-service.default.pod
4) app2-service
```

11). What name can be used to access app3 webserver by app1 pod?

12). Can you connect to app3 webserver from app1 pod using name app3-service.demo.svc.cluster?