# RBAC Assignment

1). Create a new directory say `/k8s/auth` using

```bash
sudo su -
mkdir -p /k8s/auth
```

2). Add a new csv file to this directory say `auth.csv`

```bash
echo -n "secret123,user1,u01" > /k8s/auth/auth.csv
```

3). Open the `/etc/kubernetes/manifests/kube-apiserver.yaml`

```bash
vim /etc/kubernetes/manifests/kube-apiserver.yaml
```

```yml
  command:
  - --basic-auth-file=/auth/auth.csv

  volumeMounts:
  ...
  - mountPath: /auth
    name: basic-auth
    readOnly: true
...
volumes:
...
- hostPath:
    path: /k8s/auth
  name: basic-auth

```

4). Try using the curl and you will get access error

```bash
curl -k -v -u "user1:secret123" https://localhost:6443/api/v1/pods
```

5). For listing the pods we will create a new role say `pod-viewer` in a `pod-viewer-role.yml` file

```bash
vi pod-viewer-role.yml
```

```yml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-viewer-role
  namespace: default
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list"]
```

6). Apply the role created using

```bash
kubectl apply -f pod-viewer-role.yml
```

7). To view the existing roles in the namespace use

```bash
kubectl get roles
```

8). To describe a specific role use

```bash
kubectl describe role pod-viewer-role
```

9). The next step is to link this role with a user, in our case it is the `user1`. For this create a new `pod-viewer-rolebinding.yml` file

```bash
vi pod-viewer-rolebinding.yml
```

```yml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: pod-viewer-rolebinding
  namespace: default
subjects:
- kind: User
  name: user1
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-viewer-role
  apiGroup: rbac.authorization.k8s.io
```

10). Apply the role-binding created using

```bash
kubectl apply -f pod-viewer-rolebinding.yml
```

11). To view the existing roles in the namespace use

```bash
kubectl get rolebindings
```

12). To describe a specific role use

```bash
kubectl describe rolebinding pod-viewer-rolebinding
```

13). Try to curl and get the list of pod by using the

```bash
curl -k -v -u "user1:secret123" https://localhost:6443/api/v1/pods
```

14). Do another curl this time specifying the namespace

```bash
curl -k -v -u "user1:secret123" https://localhost:6443/api/v1/namespaces/default/pods
```

15). To check the actions the user can perform on the cluster you can use the `auth can-i` command now

```bash
kubectl auth can-i get pods --as user1
kubectl auth can-i list pods --as user1
kubectl auth can-i list pods --as user1 --namespace kube-system
kubectl auth can-i list pods --as user1 --namespace kube-system
kubectl auth can-i create pods --as user1
```
