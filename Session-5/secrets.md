
# Secrets

## To convert values in base64 format : Copy output of these commands in Notepad

```bash
echo -n 'admin' | base64
```

```bash
echo -n '1f2d1e2e67df' | base64
```

## Create a Secret : secret.yaml

```yml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  username: YWRtaW4=
  password: MWYyZDFlMmU2N2Rm
```

```bash
kubectl apply -f secret.yaml
```

```bash
kubectl get secret mysecret
```

```bash
kubectl describe secret mysecret
```

## Decoding the secret

```bash
kubectl get secret mysecret -o jsonpath='{.data}'
```

```bash
echo 'MWYyZDFlMmU2N2Rm' | base64 --decode
```

## Use Secret inside a Pod : pod-secret.yaml

```yml
apiVersion: v1
kind: Pod
metadata:
  name: secret-env-pod
spec:
  containers:
  - name: mycontainer
    image: redis
    env:
      - name: SECRET_USERNAME
        valueFrom:
          secretKeyRef:
            name: mysecret
            key: username
      - name: SECRET_PASSWORD
        valueFrom:
          secretKeyRef:
            name: mysecret
            key: password
  restartPolicy: Never
```

```bash
kubectl exec secret-env-pod env
```

[K8s Documentation for Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

[Managing Secrets Using Kubectl](https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-kubectl/)

[Managing Secrets Using ConfigFile](https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-config-file/)