# Configuration - Secrets

## Get the secrets in the system

```bash
kubectl get secrets
```

## Get the details of a secret

```bash
kubectl describe secret secretName
```

## Create secret

```bash
kubectl create secret generic db-secret --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123
```

## Apply the secret to a pod

```yaml
kind: Pod
metadata:
  name: ubuntu-sleeper-2
spec:
  containers:
  - name: ubuntu
    image: ubuntu
    command: [ "sleep" ] # The command.
    args: [ "5000" ] # The arguments.
    envFrom:
    - secretRef:
        name: db-secret
```
