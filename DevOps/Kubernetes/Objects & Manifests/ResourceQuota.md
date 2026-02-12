```yaml
- name: nginx
  image: nginx:1.14.2
  resources:
	  requests: # use this amount 
		  cpu: 250m # 250 milicore
		  memory: "65M"
	  limits: # should be more than or equal to resources
		  cpu: 500m
		  memory: "130M"
```