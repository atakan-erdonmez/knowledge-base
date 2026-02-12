- docker network ls
- docker network create \<name>

When running container, you can specify the network

- `docker run -p 27017:27017 --name mongodb --network mongo-network mongo:latest`

Note: There is no such a thing as "accessing the network", only "accessing to the container". So when you create a network, containers inside can talk each other. But if you didn't bind ports to a specific container, you can't access.

Checkout here for use in [[Docker Compose]]

## Host network type
If you use `--network host` flag, you basically **remove all the isolation** and all services and ports will be accessible from the host. **


## MACVLAN network type

It connects to the LAN as they are physical devices.
You have to assign IPs manually

```
docker network create -d macvlan \
--subnet 10.0.0.0/24 \
--gateway 10.0.0.1 \
-o parent=enp0s3 \
mynetwork
```

`docker run --network mynetwork --ip 10.0.0.2 ubuntu`