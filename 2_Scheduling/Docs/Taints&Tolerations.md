---

# Taints and Tolerations

---

```bash
kubectl describe nodes kmaster | grep -i taints 
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
  tolerations:
  - key: "node-role.kubernetes.io/master"
    operator: "Exists"
    effect: "NoSchedule"
```

[Command Reference](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#taint)

[Property Reference](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#concepts)

---