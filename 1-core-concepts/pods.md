# Core Concepts - Pods

## Get the pods in the system.

```bash
kubectl get pods
```

## Create a pod with an image

```bash
kubectl run nginx --image=nginx
```

## Get details about a pod

```bash
kubectl describe pod nginx
```

## Get more details about a pod.

For example, to get on which node the pod is scheduled.

```bash
kubectl get pods -o wide
```

## Generate yaml resource from command.

```bash
kubectl run nginx --image=nginx -o yaml --dry-run=client > nginx.yaml
```

## Apply a k8s yaml resource file

```bash
kubectl apply -f nginx.yaml
```

## Delete a Pod

```bash
kubectl delete pod nginx
```
