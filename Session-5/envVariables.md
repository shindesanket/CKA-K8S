# Environment Variables

## envars.yaml

```yml
apiVersion: v1
kind: Pod
metadata:
  name: print-greeting
spec:
  containers:
  - name: env-print-demo
    image: bash
    env:
    - name: GREETING
      value: "Warm greetings to"
    - name: HONORIFIC
      value: "The Most Honorable"
    - name: NAME
      value: "Kubernetes"
    command: ["echo"]
    args: ["$(GREETING) $(HONORIFIC) $(NAME)"]
```

```bash
kubectl apply -f envars.yaml
```

```bash
kubectl get pods
```

```bash
kubectl logs print-greeting
```

[K8s Documentation for environment variables](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/)
