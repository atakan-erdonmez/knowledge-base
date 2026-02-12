Volumes are for persistent data. You create them your host, and virtually mount to the container.
The volumes are in `/var/lib/docker/volumes`

### Create volume
`docker volume create my-data`

There are 3 volume types:

Check out here for volumes in [[Docker Compose]]
### 1- Manual volumes
```
docker run 
	-v /home/mount/data:var/lib/mysql/data
```

You specify the physical location to the virtual location

### 2- Anonymous volumes
```
docker run 
	-v /var/lib/mysql/data
```

It automatically creates a folder in /var/lib/docker/volumes/<container_id>/\_data and automatically mounts to the specified location

### 3- Named Volumes (Recommended)

It is like anonymous volumes, but you specify the name instead of the full location
```
docker run 
	-v name:/var/lib/mysql/data
```

> **The actual files that are mounted to containers are in `_data` folder inside the volume**


