# Configuration - Commands and Arguments

## Execute a command with argument on Pod startup

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
```

## Force edit a property that can't change in a Pod

```bash
kubectl edit pod ubuntu-sleeper-3

# The result will be forbidden with a new file that contains the edit in the tmp directory. Then, you can force update using the following command.
kubectl replace --force -f /tmp/kubectl-edit-23213.yaml
```

## Create a pod with an argument

```bash
kubectl run webapp-green --image=kodekloud/webapp-color -- --color green
```

## Create a pod with a command and argument

```bash
kubectl run webapp-green --image=kodekloud/webapp-color --command -- python app2.py -- --color green
```
