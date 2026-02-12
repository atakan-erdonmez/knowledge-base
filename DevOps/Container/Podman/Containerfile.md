Instead of making changes inside a running container, the best practice is to define your desired state in a **`Containerfile`** (or `Dockerfile`). This is a simple text file with instructions.

A `Containerfile` for your example would look like this:

```
# Start from the base Fedora image
FROM fedora:latest

# Install the nano editor during the build process
RUN dnf -y install nano && dnf clean all

# The default command to run when the container starts
CMD ["/bin/bash"]
```

You would then build this into your own custom, reusable image: 
```
podman build -t my-custom-fedora .
```