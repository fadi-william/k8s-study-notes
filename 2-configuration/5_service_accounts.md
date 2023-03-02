# Configuration - Service Account

## Get the service accounts in the system

```bash
kubectl get sa
```

## Get details about a service account

```bash
kubectl describe sa default
```

## Create a service account

```bash
kubectl create sa dashboard-sa
```

## Mount the service account as a secret

```bash
kind: Pod
metadata:
  name: ubuntu-sleeper-2
spec:
  serviceAccountName: dashboard-sa
  containers:
  - name: ubuntu
    image: ubuntu
    command: [ "sleep" ] # The command.
    args: [ "5000" ] # The arguments.
    envFrom:
    - secretRef:
        name: db-secret
```