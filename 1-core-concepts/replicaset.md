# Core Concepts - ReplicaSet

## Get the replicasets in the system.

```bash
kubectl get replicasets
```

Note the following properties:

- Desired
- Ready
- Current 

## Get details about a replicaset

```bash
kubectl describe replicaset new-replica-set
```

## ReplicaSet yaml resource template

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset-1
spec:
  replicas: 2
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx
```

## Edit an existing ReplicaSet

```
kubectl edit rs new-replica-set
```

Note: You must delete the old pods manually in order for the changes of the replicasets take effect.

## Scale the ReplicaSet

```bash
kubectl scale rs new-replica-set --replicas=5
```
