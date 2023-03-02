# Configuration - Security Contexts

## Get which user is running the container

```bash
kubectl exec ubuntu-sleeper -- whoami
```

## Configure the pod to run its command with the user id 1010

```bash
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
    securityContext:
      runAsUser: 1010
      # runAsGroup: 3000
      # fsGroup: 2000
```

### Note: Container level user overrides pod level container.

### Example:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: multi-pod
spec:
  securityContext:
    runAsUser: 1001
  containers:
  -  image: ubuntu
     name: web
     command: ["sleep", "5000"]
     securityContext:
      runAsUser: 1002
  -  image: ubuntu
     name: sidecar
     command: ["sleep", "5000"]
```

## Add capability to the Security Contexts 

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: multi-pod
spec:
  securityContext:
    runAsUser: 1010
      capabilities:
        add: [ "SYS_TIME", "NET_ADMIN" ]
  containers:
  -  image: ubuntu
     name: web
     command: ["sleep", "5000"]
     securityContext:
      runAsUser: 1002
  -  image: ubuntu
     name: sidecar
     command: ["sleep", "5000"]
```