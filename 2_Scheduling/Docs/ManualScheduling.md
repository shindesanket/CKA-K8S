
# Demo Example :

## 1) Create a pod with redis image which always gets scheduled on worker node 2

```bash
apiVersion: v1
kind: Pod
metadata:
  name: manual-schedule-pod
spec:
  containers:
  - name: nginx
    image: nginx
  nodeName: <node-name>
```

## To Practice :

## 2) Create a pod with nginx image which always gets scheduled on worker node 1
