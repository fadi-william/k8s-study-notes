# Configuration - Taints and Tolerations

## Set a taint on a node

```sh
kubectl taint nodes node-name key=value:taint-effect
```

"taint-effect" can be as follows

1. NoSchedule
2. PreferNoSchedule
3. NoExecute

Example

```
kubectl taint nodes node1 app=blue:NoSchedule
```

## Untained a node

Example

```
kubectl taint nodes node1 app=blue:NoSchedule-
```

Note the minus at the end.

## Specify toleration on a Pod

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: myapp-pod
spec:
    containers:
    - name: nginx-container
      image: nginx
    tolerations:
    - key: "app"
      operator: "Equal"
      value: "blue"
      effect: "NoSchedule"
```
