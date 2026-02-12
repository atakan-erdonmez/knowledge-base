Podman is a daemonless container engine that is a drop-in replacement for Docker. It is developed by Red Hat and is the default container tool on Fedora. For creating isolated lab environments, it's often lighter and simpler than a full VM.

# Install
```
sudo dnf install podman
```

# Create Fedora Container
```
# Pull the latest Fedora image
podman pull fedora

# Create and start a new container named 'fedora-lab'
podman run -it --name fedora-lab fedora /bin/bash
```

### Command Breakdown

`podman run -it --name fedora-lab fedora /bin/bash`

| Parameter               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| :---------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`podman`**            | The command-line interface (CLI) for managing containers with Podman.                                                                                                                                                                                                                                                                                                                                                                                                |
| **`run`**               | The primary action command. It creates a new container from a specified image and then starts it. It's a combination of `podman create` and `podman start`.                                                                                                                                                                                                                                                                                                          |
| **`-it`**               | This is actually two separate flags combined for convenience. They are almost always used together for interactive sessions. <br><br>**`-i`** (`--interactive`): Keeps Standard Input (STDIN) open. This allows you to type commands _into_ the container.<br>**`-t`** (`--tty`): Allocates a pseudo-TTY (a terminal). This gives you a proper command prompt, allows you to use arrow keys for history, and makes the session look and feel like a normal terminal. |
| **`--name fedora-lab`** | Assigns a human-readable name, `fedora-lab`, to the container. This is highly recommended. Without it, Podman would assign a random, long string of characters. Using a name makes it much easier to manage the container later (e.g., `podman stop fedora-lab`).                                                                                                                                                                                                    |
| **`fedora`**            | This is the **image** to use as a template for the container. An image is a read-only blueprint containing the operating system, its files, and any pre-installed applications. If you don't have the `fedora` image downloaded locally, Podman will automatically pull it from a container registry (like `registry.fedoraproject.org`). This might also be written as `fedora:latest` to specify the "latest" version.                                             |
| **`/bin/bash`**         | This is the **command** to execute inside the container after it starts. In this case, you are starting the Bash shell. Because you used the `-it` flags, you are directly connected to this shell, allowing you to run commands interactively.                                                                                                                                                                                                                      |

# Managing Container

- To exit the container's shell: `exit`
- To list all containers (running and stopped): `podman ps -a`
- To start the container again: `podman start fedora-lab`
- To attach to a running container: `podman attach fedora-lab`
- To start and attach a stopped container: `podman start -ai fedora-lab`