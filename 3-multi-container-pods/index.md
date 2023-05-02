# Multi-Container Pods

## Patterns

- SideCar
- Adapter
- Ambassador

## Examples

### Multi-Container Pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  name: yellow
spec:
  containers:
  - image: busybox
    name: lemon
    command: [ "sleep", "1000" ]
  - image: redis
    name: gold
```

### Init Container

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  name: red
spec:
  initContainers:
  - image: busybox
    name: red-init-container
    command: [ "sleep", "20" ]
  containers:
  - image: busybox
    name: lemon
    command: [ "sleep", "1000" ]
  - image: redis
    name: gold
```
