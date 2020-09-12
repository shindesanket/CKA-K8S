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
      tolerations:
      # this toleration is to have the daemonset runnable on master nodes
      # remove it if your masters can't run pods

      containers:
      - name: nginx
        image: nginx:alpine
        # request and limit memory to 200Mi
        # request cpu to 100m
```

---