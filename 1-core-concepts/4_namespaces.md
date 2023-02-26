# Core Concepts - Namespaces

## Get the namespaces in the system

```bash
kubectl get namespaces
```

or 

```bash
kubectl get ns
```

## Get the pods in a namespace

```bash
kubectl get pods -n default
```

## Create a Pod in a namespace

```bash
kubectl run redis  --image=redis -n finance
```

## Get all the pods in all the namespaces

```bash
kubectl get pods --all-namespaces 
```

```bash
kubectl get pods -A
```

## Access a service in the same namespace

- The service name is sufficient to be resolved by the k8s DNS.

## Access a service in another namespace

- The service name should follow a specific structure which is `serviceName.namespaceName.svc.cluster.local`