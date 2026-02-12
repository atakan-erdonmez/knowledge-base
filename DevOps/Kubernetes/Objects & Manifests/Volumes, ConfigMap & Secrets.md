It is an object type that you put pieces of data like configuration files and environment variables.

`kubecctl create configmap NAME --from-file=FILE` -> create a quick configmap
`kubectl get configmaps` -> Show configmaps 
`kubectl describe cm NAME` -> Describe cm (configmap)

## Adding a ConfigMap Permanently

```yaml
# Same indentation with 'containers:'
spec:
	containers:
	- name: nginx
	  image: nginx:1.14.2
	  volumeMounts:
	  - name: my_vol
	    mountPath: /hbroes

	volumes:
	  - name: my_vol
	    configMap:
		    name: heroes
```

**Note**: K8s will create folders if they don't exist. '/heroes' will be created automatically
**Another Note:** The folder will be OVERWRITTEN. To prevent it, you can use *subPath*.

# Secrets
They are a separate object type.
```yaml
apiVersoin: v1
kind: Secret
metadata:
	name: mysql-secret
type: kubernetes.io/basic-auth
stringData:
	password: deneme
```

(You can also use command line `kubectl create secret generic NAME --type=kubernetes.io/basic-auth --from-literal=password=deneme`)

- `kubectl get | describe secrests [SECRET_NAME]`

## Using Secret inside Manifest

```yaml
spec:
  containers:
  - image: mysql:8-debian
    name: mysql
    env:
	- name: MYSQL_ROOT_PASSWORD
	  valueFrom: 
	    secretKeyRef:
	      name: mysql-secret
	      key: password # look for this key-value
```