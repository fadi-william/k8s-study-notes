# Pod Design

## Labels & Annotations as Metadata

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: simple-webapp
    # Label K8s Resources.
    labels:
    	name: simple-webapp
        function: front-end
    # Annotation is used for information purposes.
    # With operators, it can enable features.
    annotations:
        buildVersion: 1.34
```

### Select pods with labels

```sh
kubectl get pods --selector function=front-end
```

### Notes

1. Labels defined for the pods are used by the replicasets and the deployments for discovery.
2. Labels for the replicasets and deployments are used by the service for discovery.

## Rollout

### Get status

```sh
kubectl rollout status deployment/myapp-deployment
```

### Get history

```sh
kubectl rollout history deployment/myapp-deployment
```

### Get revision

```sh
kubectl rollout history deployment nginx --revision=1
```

### Record the change cause

```sh
kubectl set image deployment nginx nginx=nginx:1.17 --record
```

### Updating deployments

Rolling update will be applied once deployment is modified using the k8s apply of the modifications.

```sh
kubectl apply -f deployment-modified-definition.yml
```

### Revert a deployment

```sh
kubectl rollout undo deployment/myapp-deployment
```

### Revert to a specific version

```sh
kubectl rollout undo deployment nginx --to-revision=1
```

### Updating a deployment image

```sh
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
```

### Deployment strategies

1. Recreate
2. Rolling Update (Default)

## Jobs

### Job Definition

```yaml
apiVersion: batch/v1
kind: Job
metadata:
    name: math-add-job
spec:
    completions: 3
    # To parallelize the tasks,
    # You can use the following property.
    parallelism: 3
    template:
        spec:
            containers:
                - name: math-add
                  image: ubuntu
                  command: ['expr', '3', '+', '2']
            restartPolicy: Never
```

### Cron Job

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
    name: reporting-cron-job
# Spec for cron job.
spec:
    schedule: '*/1 * * * *'
    jobTemplate:
        # Spec of the job template.
        spec:
            # To parallelize the tasks,
            completions: 3
            # You can use the following property.
            parallelism: 3
            template:
                spec:
                    # Spec of the pod.
                    containers:
                        - name: reporting-tool
                          image: reporting-tool
                    restartPolicy: Never
```
