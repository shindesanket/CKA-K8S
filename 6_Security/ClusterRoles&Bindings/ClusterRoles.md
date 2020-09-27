
# Cluster Roles and Cluster Bindings

Check namespaced resources :

```bash
kubectl api-resources --namespaced=true
```

Check cluster scoped resources :

```bash
kubectl api-resources --namespaced=false
```

```bash
vi pv-clusterrole.yaml
```

```yml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: pv-clusterrole
rules:
- apiGroups: [""]
  resources: ["persistentvolumes"]
  verbs: ["create", "list", "delete"]
```

```bash
vi pv-clusterrolebinding.yaml
```

```yml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: pv-clusterrolebinding
subjects:
- kind: User
  name: user1
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: pv-clusterrole
  apiGroup: rbac.authorization.k8s.io
```

```bash
kubectl auth can-i get persistentvolumes --as user1
kubectl auth can-i create persistentvolumes --as user1
```
