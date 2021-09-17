# DaemonSets

---

[Reference Link](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

```yml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: nginx-ds
  namespace: kube-system
  labels:
    k8s-app: nginx
spec:
  selector:
    matchLabels:
      name: nginx
  template:
    metadata:
      labels:
        name: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:alpine
```

---
