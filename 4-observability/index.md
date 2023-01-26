# Observability

## Readiness Probe

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp
    labels:
    	name: simple-webapp
spec:
    containers:
    - name: simple-webapp
      image: simple-webapp
      ports:
        - containerPort: 8080
      # Ready is true once readiness probe is successful.
      readinessProbe:
        # Http Example
        httpGet:
            path: /api/ready
            port: 8080
        # TCP Example
        tcpSocket:
            port: 3306 
        # Command Example
        exec:
            command:
                - cat
                - /app/is_ready
        # When to start to probe.
        initialDelaySeconds: 10
        # How often to probe.
        periodSeconds: 5
        # By default, probe will stop after 3 attempts. 
        # However, we can increase the number of attemtps
        # by the following property.
        failureThreshold: 8
```

## Liveness Probe

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp
    labels:
    	name: simple-webapp
spec:
    containers:
    - name: simple-webapp
      image: simple-webapp
      ports:
        - containerPort: 8080
      # Make sure that the app/service is running 
      # and healthy
      livenessProbe:
        # Http Example
        httpGet:
            path: /api/healthy
            port: 8080
        # TCP Example
        tcpSocket:
            port: 3306 
        # Command Example
        exec:
            command:
                - cat
                - /app/is_healthy
        # When to start to probe.
        initialDelaySeconds: 10
        # How often to probe.
        periodSeconds: 5
        # By default, probe will stop after 3 attempts. 
        # However, we can increase the number of attemtps
        # by the following property.
        failureThreshold: 8
```

## Logging

### For Pods with a single container

```sh
kubectl logs -f event-simulator-pod
```

### For Pods with multiple containers

```sh
kubectl logs -f event-simulator-pod  event-simulator-container
```

## Monitoring

### The metrics server

Enable in Minikube via `minikube addons enable metrics-server`. Otherwise, use Github Yaml Files.

### Commands

#### Check Memory and CPU for Nodes.

```
kubectl top node
```

#### Check Memory and CPU for Pods

```
kubectl top pod
```
