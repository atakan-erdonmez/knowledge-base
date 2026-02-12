You need:
- Persistent volume
- Persistent volume claim

You assign the 'claim' to the container, which then can access the volume.

## Storage Class
After you create your storage solution, you create a Storage Class for K8s to recognize it and use it as a storage solution.

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
	name: alta3-pv
spec:
	storageClassName: manual # type
	capacity:
		storage: 2Gi
	accessModes:
	- ReadWriteOnce # only 1 node can add as RW
    hostPath: 
	    path: "/mnt/data"
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
	name: nginx-pvc
spec:
	storageClassName: manual
	accessModes:
	- ReadWriteOnce
    resources:
	    requests:
		    storage: 1Gi
```

To add it to a pod:
```yaml
spec:
	containers:
	...
		volumeMounts:
		- name: nginx-pv-storage
		  mountPath: "/data"
	volumes:
	- name: nginx-pv-storage
	  persistentVolumeClaim:
		  claimName: nginx-pvc
```