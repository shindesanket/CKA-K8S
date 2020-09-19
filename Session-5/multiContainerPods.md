# Multi Containers Pod

## Create a pod using 2 containers : two.yaml

```yml
apiVersion: v1
kind: Pod
metadata:
  name: two-containers
spec:

  restartPolicy: Never

  volumes:
  - name: shared-data
    emptyDir: {}

  containers:

  - name: nginx-container
    image: nginx
    volumeMounts:
    - name: shared-data
      mountPath: /usr/share/nginx/html

  - name: debian-container
    image: debian
    volumeMounts:
    - name: shared-data
      mountPath: /pod-data
    command: ["/bin/sh"]
    args: ["-c", "echo Hello from the debian container > /pod-data/index.html"]
```

```bash
kubectl apply -f two.yaml
```

```bash
kubectl exec -it two-containers -c nginx-container -- /bin/bash
```

```bash
apt-get update
apt-get install curl procps
ps aux
curl localhost
```
