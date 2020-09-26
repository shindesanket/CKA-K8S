
# ImageSecurity

```bash
kubectl run nginx-demo --image=democka.azurecr.io/samples/nginx:latest --dry-run=client --restart=Never -o yaml > nginx-pod.yaml
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
kubectl create secret docker-registry myregistrykey --docker-server=democka.azurecr.io \
        --docker-username=democka --docker-password=PgGaSLOIMuVw3M9m7+qzYoAxmxDGPt13 \
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
  - image: democka.azurecr.io/samples/nginx:latest
    name: nginx-demo
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

```bash
kubectl apply -f nginx-pod.yaml
```
