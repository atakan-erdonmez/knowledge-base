# Create a Container Network
```
podman network create lab_net
podman network ls
```

# Add Container to the Network
Now, when you create your containers, you simply need to add the `--network lab_net` flag to attach them to your new network.

Let's create two Fedora containers, `server-app` and `client-app`, and attach them both to `lab_net`.

- **Run the first container (server-app):** We'll run this in detached mode (`-d`) so it stays running in the background.

```
podman run -dt --name server-app --network lab_net fedora
```

- **Run the second container (client-app):** We'll start this one interactively so we can immediately test the connection.

```
podman run -it --rm --name client-app --network lab_net fedora /bin/bash
```

Notice the `--rm` flag here. This is a handy option that automatically removes the container when you exit its shell, keeping your environment clean.

# Check Network Connectivity
```
dnf install -y iputils # Installs ping
ping server-app
```