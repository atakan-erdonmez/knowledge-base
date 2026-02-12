Stack is a bunch of services running in multiple devices. Basically running a compose file in a Swarm.

## Create a Stack
You can use a regular compose file with some addition
```
docker stack deploy -c stack.yml my-wordpress-app
```
## Stack Management
- `docker stack ls`: List all running stacks.
- `docker stack services my-wordpress-app`: List all services within that stack.
- `docker stack ps my-wordpress-app`: See all the running tasks for the stack.
- `docker stack rm my-wordpress-app`: Remove the entire stack and all its services.


