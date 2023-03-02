# Configuration - ConfigMaps

## Get the ConfigMaps in the default namespace

```bash
kubectl get cm
```

## Get details of a ConfigMap

```bash
kubectl describe cm db-config
```

## Create a ConfigMap from literal

```bash
kubectl create cm webapp-config-map --from-literal=APP_COLOR=darkblue
```

## Change the env value to a value from a configmap.

From:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-sleeper-2
spec:
  containers:
  - name: ubuntu
    image: ubuntu
    command: [ "sleep" ] # The command.
    args: [ "5000" ] # The arguments.
    env:
    - name: APP_COLOR
      value: green
```

To: 

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
    env:
    - name: APP_COLOR
      valueFrom:
        configMapKeyRef:
          name: webapp-config-map
          key: APP_COLOR
```
