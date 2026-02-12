Docker Swarm is a container orchestration tool that has 1 manager and multiple worker nodes.
## Create & Add Workers
`docker swarm init --advertise-addr IP` -> Create a swarm with that machine being manager

`docker swarm join --token TOKEN IP:PORT` -> Add workers to the swarm

## Leave the Swarm
`docker swarm leave [--force]` (ON NODE)-> Leave the swarm, flag is not necessary
- Shows the node as "Down" in Manager
`docker node rm [-f] <node-id>` (ON LEADER) -> Remove the node from the swarm. 
- Leave first, remote after. -f forces to remove before node leaving itself

> Note: Forcefully removing a node creates problems, like node not knowing it is not a part of the swarm. **Not Recommended**

To completely destroy a swarm, the last remaining node, which is a manager, should leave --force
## Information
- `docker info` shows info about swarm.
- `docker node ls` -> Show node info
# Services
## Start & Stop

`docker service create --name <name> --replicas <how many instance> -p 80:80 nginx`
- This creates a service

`docker service rm <name>` 
- This removes the service

`docker service inspect [--pretty] <service-name>` 
- Inspects the service, shows info like parallelism, IP etc

`docker service ps <service-name>`
- Shows which nodes runs the service

> [!Note]
> When you create a service with replicas, you can reach that service from every node **even when that specific node doesn't run that container**. This is because of ingress routing mesh, which provide access even when a node is down. It creates high-availability and load-balancing

## Services Info
`docker service ls` -> Shows service info

*When you stop a container in a working node, the manager automatically restarts*
## Scaling
`docker service scale web-server=5` -> Scale up to 5 replicas
`docker service ls` -> show the services
`docker service ps <service>` -> show the replicas

# Updates
`docker service create --replicas 3 --name redis --update-delay 10s redis:8.0`
`docker service update --image redis:8.2 redis` -> updates to 8.2

**Warning**: If the update name is wrong, that replica stops

> [!Note]
> You can put `--update-delay 10s` when creating service to delay the update


# Draining Node
Draining means stopping this node from getting any tasks for maintenance or planned shutdown.
`docker node update --availability drain <id>`

If there are containers on that node, it will transferred to another node

`docker node update --availability active <id>`

# Networking
Overlay network: It is used to connect different docker daemons together. It is mostly used in Swarm, but can be used to connect standalone containers. [DockerHub](https://docs.docker.com/engine/network/drivers/overlay/)

## Create a Network

`docker network create --driver overlay my-network`
`docker service create --replicas 3 --network my-network --name test nginx:latest`

`docker service inspect test --pretty`

## Add to a Network

`docker service update --network-add my-network test`
`docker service update --network-rm my-network test`

These commands are used to add/remove a network from a service

# Storage
You can either add volume while creating or afterwards.

## Update (Add Later)
`docker service update --mount-add type=volume,source=new-vol,target=/app test`
## Create (While Creating)
`docker service create --mount source=new-vol,target=/app -name myservice <image>`

Note: You can also bind mount instead of volume mount, which is mounting a specific folder. Not suggested