# Services & Networking

## NodePort

The node port range is from 30000 - 32767.

```yaml
apiVersion: v1
kind: Service
metadata:
    name: app-service
spec:
    type: NodePort
    ports:
        - targetPort: 80
          # If not provided. Will be the same as the target port.
          port: 80 
          # If not provided. An automatic available port will be allocated.
          nodePort: 30008 
    selector:
        app: myapp
        type: front-end
```

### Notes: 

- The selector algorithm is random, when the selector matches multiple pods on the same node.
- The service is created across the different nodes that host the pods with the service's matching pod selector. So, you can access the pods via the nodeport on any of the nodes that host a matching pod via its ip.

## Cluster IP

For communication within the cluster.

```yaml
apiVersion: v1
kind: Service
metadata:
    name: backend
spec:
    # The cluster ip is the default type. So, next property could be skipped.
    type: ClusterIP 
    ports:
        - targetPort: 80
          port: 80 
    selector:
        app: myapp
        type: front-end
```

## Ingress

### Ingress Samples

#### Example 1

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
    name: ingress-wear
spec:
    backend:
        serviceName: wear-service
        servicePort: 80
```

#### Example 2

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
    name: ingress-wear
spec:
    rules:
    - host: wear.online-store.com
      http:
        paths:
        - path: /wear
          backend:
            serviceName: wear-service
            servicePort: 80
     - host: watch.online-store.com
       http:
        paths:
        - path: /watch
          backend:
            serviceName: watch-service
            servicePort: 80
```

Ingress's new update yaml api: https://bm-digitalacademy.udemy.com/course/certified-kubernetes-application-developer/learn/lecture/28046958#overview

## Network Policy

An example on how to define a network policy.

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
      matchLabels:
        name: api-pod
    ports:
    - protocol: TCP
      port: 3306
```
