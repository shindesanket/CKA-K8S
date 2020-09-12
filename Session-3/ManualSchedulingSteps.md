# Manual Scheduling a POD

---

1. Create a pod template

```bash
# create a pod template using the command for our playground environment
kubectl run nginx-pod --image=nginx:alpine --restart=Never --dry-run -o yaml > nginx-pod-manual-scheduling.yaml

# create a pod template using the command  for v1.18
kubectl run nginx-pod --image=nginx:alpine --dry-run=client -o yaml > nginx-pod-manual-scheduling.yaml

```

2. Open the `nginx-pod-manual-scheduling.yaml` file and modify it contents -

```bash
vim nginx-pod-manual-scheduling.yaml
```

```yml
# add the below in the spec section of pod
spec:
  nodeName: <SPECIFY-NODE-NAME-HERE>
```

3. Deploy your configuration using the command -

```bash
kubectl apply -f nginx-pod-manual-scheduling.yaml
```

4. To check the pod has been deployed on specified node name use -

```bash
# check the node name where the above pod is deployed
kubectl get pods -o wide 
```

5. To delete the pod use -

```bash
kubectl delete -f nginx-pod-manual-scheduling.yaml
```

---