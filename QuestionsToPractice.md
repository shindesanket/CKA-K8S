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