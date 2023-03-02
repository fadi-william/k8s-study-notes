# Configuration - Resource Requirements

## Specific Resource Limit and Quotas

```yaml
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
   resources:
      limits:
        cpu: 2
        memory: 20Mi
      requests:
        cpu: 1
        memory: 5Mi
```
