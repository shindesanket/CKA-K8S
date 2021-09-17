# Resource Requirements and Limits

---

[Reference Link](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory)

[Additional Reference](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/)

---

## Example

```bash
apiVersion: v1
kind: Pod
metadata:
  name: frontend
spec:
  containers:
  - name: app
    image: images.my-company.example/app:v4
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```
