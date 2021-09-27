
# ImageSecurity

```bash
kubectl run nginx-demo --image=aksdemo123.azurecr.io/shindesanket/delphimeproject:15 --dry-run=client --restart=Never -o yaml > nginx-pod.yaml
```

```bash
kubectl apply -f nginx-pod.yaml
```

```txt
Observe POD is not running due to image pulling error
```

```bash
kubectl delete pod nginx-pod
```

```bash
kubectl create secret docker-registry myregistrykey --docker-server=aksdemo123.azurecr.io \
        --docker-username=aksdemo123 --docker-password=xv7UQMMgv60==/sAZnSLQSfxm6eQKQoe \
        --docker-email=DUMMY_DOCKER_EMAIL
```

```bash
vi nginx-pod.yaml
```

```yml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx-demo
  name: nginx-demo
spec:
  imagePullSecrets:
  - name: myregistrykey
  containers:
  - image: aksdemo123.azurecr.io/shindesanket/delphimeproject:15
    name: nginx-demo
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

```bash
kubectl apply -f nginx-pod.yaml
```
