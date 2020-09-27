# NodeSelector and Node Affinity

---

```bash
kubectl label nodes kmaster machine=control-plane
```

```yml
apiVersion: v1
kind: Pod
metadata:
  name: k8s-bootcamp-pod
  labels:
    app: k8s-bootcamp-app
spec:
  containers:
  - name: k8s-bootcamp-container
    image: gcr.io/google-samples/kubernetes-bootcamp:v1
    ports:
    - containerPort: 8080
  nodeSelector:
    machine: control-plane
```

```yml
apiVersion: v1
kind: Pod
metadata:
  name: k8s-bootcamp-pod
  labels:
    app: k8s-bootcamp-app
spec:
  containers:
  - name: k8s-bootcamp-container
    image: gcr.io/google-samples/kubernetes-bootcamp:v1
    ports:
    - containerPort: 8080
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: machine
            operator: In
            values:
            - control-plane
```

[Reference Link](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector) 