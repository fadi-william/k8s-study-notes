# Volumes

## Persistent Volumes

### Example

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
    name: pv-vol1
spec:
    accessModes:
        # ReadOnlyMany, ReadWriteOnce, ReadWriteMany
        - ReadWriteOnce
    capacity:
        storage: 1Gi
    hostPath:
        path: /tmp/data
```

## Persistent Volume Claim

### Example

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
    name: myclaim
spec:
    accessModes:
    - ReadWriteOnce
    resources:
        requests:
            storage: 500Mi
```

#### Notes

* You can choose what to do on persistent volume claim deletion using the `persistentVolumeReclaimPolicy` to `Delete`, or `Retain`, or `Recycle`.
