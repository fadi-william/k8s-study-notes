# Configuration - Node Selector

## Assign Labels to Nodes

```sh
kubectl label nodes node-name label-key=label-value
```

### Example

```sh
kubectl label nodes node-1 size=Large
```

## Assign a Pod on a node with a label 

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
    nodeSelector:
        size: Large
```
