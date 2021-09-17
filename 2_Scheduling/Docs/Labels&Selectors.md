
## 1) Create a pod :
   Name : nginx, Image : nginx, Label : type=webServer and tier=frontEnd

## 2) Create a pod :
   Name : redis, Image : redis, Label : type=cache
  
Hint : Use below command to generarte pod manifest 

```bash
kubectl run pod nginx-demo --image nginx --dry-run=client -o yaml > nginx.yaml
```

Observe the output of following commands :

```bash
kubectl get pods --selector type=cache
```

```bash
kubectl get pods --selector type=webServer,tier=frontEnd
```
