- docker images: It will show every downloaded docker images that exist in local
- docker search \<name>: Search for a docker container in the Docker repo
- **docker pull \<name>**: Pull the image, which is downloading
- docker run \<image_name>: Create a container from the pulled image
- docker stop \<image>: Stop the container
> Note: When you run a docker container and they don't have anything to do, they exit automatically.

- docker ps: List all running containers
- docker ps -a: List all containers, both running and exited

**NOTE**: Containers don't save changes. Docker images are just blueprints. After you create a container from it and exit it, it deletes everything and goes back to the default image.

> [!Command]
> `docker run -it ubuntu bash`
-i -> interactive (keeps STDIN open)
-t -> allocates a pseudo-TTY (terminal)
This way, you can start the container and interact with it

> You can give names to containers via --name flag
### Permanent & Temporary Containers
- ***-d:*** Daemon mode, sends to background
- docker attach \<container_ID> : Attach a background container to the terminal

- **To exit without shutting down**, you can `^P` + `^Q` to exit gracefully.

> When you are referencing a container ID, you can just specify the first couple of string, and Docker can understand 


**Entrypoint command:** A command that starts automatically in the container

### Accessing Apps & Ports

Normally, you can't access the containerized apps via TCP/IP stack by default, ports are not open to external access. You need to forward ports for that.

- ***-p 8080:80***: Directs port 8080 of external to 80 of internal. Which means, when you go to container:8080, it will redirect to port 80 of the container
	`docker run -it -d -p 8080:80 nginx`

> You might need to stop/start services via `/etc/init.d/nginx start`
### Running Mission-critical Containers
- ***--restart***: This flags tells the container to restart itself based on the policy
###### Policies:
- `no` → (default) never restart automatically.
- `always` → always restart, even if you manually stop it (it will come back up after Docker restart).
- `on-failure` → restart only if the container exits with a non-zero exit code (you can also limit retries with `on-failure:N`).
- `unless-stopped` → restart automatically **unless you stopped it yourself**.

### Creating Images
You can create container images from running containers.

- docker commit \<container_ID> \<name>:  Create an image same as the running container. 
	`docker commit <cont_ID> atakan/apache-test:1.0`
	
	Then you can check with `docker images`

Run with: `docker run -d -it -p 8080:80 atakan/apache-test:1.0`


#### Entrypoint
When you are creating an image from a container, there is something you should be aware of: Entrypoint

Entrypoint is a parameter you might need to define when committing. It basically is a command to run automatically when the container is started.

You should create an entrypoint to run the service and put it in the foreground. Normally, the service is inactive, you will need to start manually.

**IMPORTANT NOTE**: When you are defining entrypoint, you should *ALWAYS* run the service in the foreground to keep the container open

###### Examples:
- `docker commit --change='ENTRYPOINT ["apachectl", "-DFOREGROUND"] <container_ID> <name>`
- `docker commit --change=ENTRYPOINT ["nginx", "-g", "daemon off;"]' <container_ID> <name>``

### Dockerfile
Committing is not a preferred way in Docker. You should use [[Dockerfile]]

#### Docker Commit vs. Dockerfile

^4b7fc7

| Feature             | `docker commit`                                                                                                                                                                                                         | **Dockerfile** (Recommended)                                                                                                                                                                                              |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Reproducibility** | **Low.** It's a snapshot of a container's state at a single moment. It doesn't show you the steps taken to create it. If you need to make a small change later, you have to start over and repeat all the manual steps. | **High.** It's a script with all the commands to build your image. Anyone can run `docker build` and get the exact same image. This is crucial for consistency.                                                           |
| **Auditability**    | **None.** You have no record of the commands used to modify the container, install software, or configure settings. You only know the final state.                                                                      | **Full.** The Dockerfile serves as documentation. It clearly lists every instruction, like `RUN apt-get update` or `COPY`, which makes it easy to understand what's inside the image.                                     |
| **Layers & Size**   | Can create a larger, less optimized image. It saves all file changes, including temporary files, logs, and cache from your manual work inside the container.                                                            | **Optimized.** Docker can intelligently manage layers. For example, by combining `apt-get update` and `apt-get install` in a single `RUN` command, you can minimize the number of layers and reduce the final image size. |
| **Maintainability** | **Difficult.** If you want to change one small thing, like the NGINX version, you have to do all the manual steps again. This is prone to human error.                                                                  | **Easy.** You just need to edit one line in the Dockerfile and rebuild the image. This is why it's considered a best practice for DevOps and development teams.                                                           |

^134809

### Removing Containers & Images
docker rm: Remove container
docker rmi: Remove image

##### rm flags
-f -> force
-l -> remove link
-v -> remove anonymous volumes
### Docker Logs

You can run `docker logs <cont_ID>` to print the logs of the container to the terminal.

### Docker Exec

`docker exec` is used to run a process **inside a running container**. Like you can run a CLI in a working container with:
```
docker exec my-webserver bash
docker exec -it my-server /bin/sh (???)
```

### Docker start-stop
`docker run` and `docker start` are different. 'run' is dealing with images, creating a container from an image. 'start' is actually starting a already-created container that has been stopped.

`docker stop` to stop

### Docker Inspect
### Docker info

### Environmental Variables
-e flag is used for environment variables, which passes those arguments to the container app


