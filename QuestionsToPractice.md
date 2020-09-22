# Questions to Practice

```txt
1) Ensure a single instance of pod "redis" is running on each node of k8s cluster where Image=redis. Do not override existing taints.
   Name of kubernetes object to create : ds-123
```

```txt
2) Schedule a pod with image nginx and node selector : color=blue
```

```txt
3) Create a deployment "nginx-deploy" with container nginx with version 1.10.2-alpine. Deployment should contain 5 replicas.
   Next deploy the new version 1.13.0-alpine by performing a rolling update
   finally rollback that version again to 1.10.2-alpine
```

```txt
4) Create a pod called as front-end with image nginx with label tier=front-end.
   expose this pod with cluster-IP service called as front-end-service
```

```txt
5) Create a pod nginx with image nginx in new namespace called as demo
```

```txt
6) Create a deployment spec file with following details :
   replicas : 7
   image : redis
   label : app=test
   deploymentName : deploy123

   store this spec file at etc/kubernetes/deploy.yaml
```

```txt
7) Create nginx and redis pods. List pods with the nodes information and store json format to file etc/kubernetes/pods.json
```

```txt
8) Create a nginx deployment and scale the deployment to 10 recording the history. Copy history to file etc/kubernetes/deploy-history.yaml
```

```txt
9) Create a static pod nginx with image nginx only on worker node 2  
```

```txt
10) Create a pod nginx with image nginx. Monitor the logs of nginx pod. copy these logs to nginx-logs.txt file.
```

```txt
11) Label the worker-1 node of your cluster with rack=qa.
```

```txt
12) Create a pod with 2 containers. One mainApp with busybox:1.28 image and other initContainer with busybox image.
initContainer will create empty file abc.txt in etc/kubernetes folder. Main app should check if abc.txt is present at specified folder else it should exit.
```

```txt
13) create a pod with 4 container with 4 images of your choice and store list of pods in pods-list.txt files with information of nodes.
```

```txt
14) Create a secret named as secret123 with data "firstname: scott". Create a pod named pod-using-secret using nginx image which exports firstname as SUPERSECRET
```

```txt
15) Drain worker-2 and create nginx deployment with 10 replicas. Store the list of pods with node name in nginx-pods.txt
```

```txt
16) store the current CPU and memory usage details of all nodes in usage.txt
```

```txt
17) Take current snapshot of etcd server and store it as etcd-backup.db at etc/kubernetes/etcdbackup
```

```txt
18) Create a redis deployment with 13 replicas and make worker-node1 as unavailable and reschedule all pods on it to other active nodes.
```

```txt
19) Add taint on worker-node2 as app=blue with noschedule policy
```
