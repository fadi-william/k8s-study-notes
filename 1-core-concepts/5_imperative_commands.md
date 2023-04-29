# Core Concepts - Imperative Commands

## Create a pod with an image and a label

```bash
kubectl run redis --image=redis:alpine --labels="tier=db"
```

## Create a service

### Cluster IP

```bash
kubectl expose pod redis --port=6379 --name redis-service
```

### NodePort

```bash
kubectl create service nodeport nginx --tcp=80:80 --node-port=30080
```

## Create a deployment

```bash
kubectl create deployment webapp --image=kodekloud/webapp-color --replicas=3
```

## Create a pod and expose it through container port 8080

```bash
kubectl run custom-nginx --image=nginx --port=8080
```

## Create a new namespace

```bash
kubectl create ns dev-ns
```

## Create a deployment in a namespace

```bash
kubectl create deployment redis-deploy --image redis:latest -n dev-ns
```

## Create a pod and expose it directly through a cluster ip service

```bash
kubectl run httpd --image httpd:alpine --port 80 --expose=true
```
