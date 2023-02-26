# Core Concepts - Deployments

## Get the deployments in the system.

```bash
kubectl get deployments
```

## Deployment yaml definition

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-1
spec:
  replicas: 2
  selector:
    matchLabels:
      name: busybox-pod
  template:
    metadata:
      labels:
        name: busybox-pod
    spec:
      containers:
      - name: busybox-container
        image: busybox
        command:
        - sh
        - "-c"
        - echo Hello Kubernetes! && sleep 3600
```

## Create a deployment

```
kubectl create deployment httpd-frontend --image=httpd:2.4-alpine --replicas=3
```
