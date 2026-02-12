Compose is an easy way to run Docker containers. Instead of running each container with their arguments, it is easier to prepare a compose file.



## Structure
It starts with version: tag, which is Docker Compose version.
Then, you put services: which means each containers
Then, you have the name of the container
You then have the image and options

mongo
```yaml
services:
	mongodb:
		image: mongo
		ports:
		- 27017:27017
		environment:
		- MONGO.._USERNAME=admin
		restart: unless-stopped
		
		volumes:
			- deneme:/var/lib
		networks:
			- deneme4
volumes:
	- deneme
networks:
	- deneme4
```

Note: You don't need to create a network in Compose. It will

### Start & Stop

`docker compose -f mongo.yaml up|down -d`

### Networking

You can put networks: flag to create and name the network
```
services:
	db:
		image:
		networks:
networks:
	my_network:
		name: my_custom_network1
```

### Volumes
You should put the volumes inside the services. But you should also **put them in the end of the file, same indentation with 'services:'**. 
```
# (inside services)
	volumes:
		- db-data:/var/lib/mysql/data
	  
	  
# (outside services)
volumes:
	db-data:
```
> The volume defining should be in the same level as `services:`


driver: ???

The volumes are in `/var/lib/docker/volumes`


#### Single file
To put a single file, you can use this
```
proxy:
	image: nginx
	volumes:
		- ./nginx.conf:/etc/nginx/nginx.conf
```
When done like this, you don't have to define the volume at the end of the YAML file.
### Build

Instead of manually building Dockerfiles, compose can build the existing Dockerfile for you.

You should use `build:` instead of `images:` when building an image yourself.

Example:
```
services:
	web:
		build: ./frontend
		ports:
		- "80:80"
```

Note: If you use "build:", you need to run command `docker compose up --build`. It is very important if you did any changes in the Dockerfile, since it should re-build it.

## Misc Flags

#### depends_on:
It makes a dependency to start a specific service without one. Defined under the services
```
services:
	api:
		depends_on:
			- db
```
> It only checks if the container is running, it is not a health check

#### restart:
![[Docker Management#Running Mission-critical Containers]]


#### container_name
`container_name: my_name`