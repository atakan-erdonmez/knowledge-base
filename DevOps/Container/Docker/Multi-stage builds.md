### What Is a Multi-Stage Build?

A multi-stage build uses multiple `FROM` statements in a single `Dockerfile`. Each `FROM` command starts a new build stage. You can then selectively copy artifacts—like compiled binaries or installed dependencies—from one stage to the next, leaving all the temporary files and build tools behind.

Think of it like a construction process. In the first stage (the "builder"), you bring in all the heavy machinery and tools to assemble a product. In the second stage (the "runner"), you only take the finished product and put it in a clean, lightweight box, discarding all the tools and raw materials.

---

### The Two Stages

Your `Dockerfile` will be split into two main parts:

#### The Builder Stage

This is the first stage. Its job is to perform all the dependency installation. It's named using `AS builder` to be easily referenced later. This stage can use a larger base image like `python:3.10-slim-buster` because it has the necessary build tools and packages.



```dockerfile
# Stage 1: The Builder
FROM python:3.10-slim-buster AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
```

#### The Runner Stage

This is the final stage. Its job is to create the production-ready image. It uses a much smaller base image like `python:3.10-slim` that contains only the bare essentials to run Python. Crucially, it uses the `COPY --from=builder` command to copy only the necessary files from the first stage.



```dockerfile
# Stage 2: The Final, Runner Image
FROM python:3.10-slim
WORKDIR /app
COPY --from=builder /usr/local/lib/python3.10/site-packages /usr/local/lib/python3.10/site-packages
COPY app.py .
CMD ["python", "app.py"]
```

---

### The Result

By using this multi-stage approach, your final image will be significantly smaller. You can verify this by running `docker images` before and after the build. The first stage's image, with all the heavy dependencies, is discarded, and the final image only contains your Python application and its required libraries. This not only saves disk space but also reduces the attack surface, making your image more secure.
```dockerfile
# Stage 1: The Builder
FROM python:3.10-slim-buster AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Stage 2: The Final, Runner Image
FROM python:3.10-slim
WORKDIR /app
COPY --from=builder /usr/local/lib/python3.10/site-packages /usr/local/lib/python3.10/site-packages
COPY app.py .
CMD ["python", "app.py"]
```

requirements.txt -> flask
#### Why It's a Best Practice

1. **Reduced Image Size:** As you know, a smaller image is faster to download and deploy. A multi-stage build gets rid of unnecessary build tools (like compilers, development headers, or even the package manager's cache) that are only needed to create the application but not to run it.
    
2. **Improved Security:** This is a crucial benefit. If you include development tools or temporary files in your final image, you're also including potential vulnerabilities. A smaller image has a smaller **attack surface**, as it contains only the bare minimum needed for the application to function.
    
3. **Cleaner Layers:** Each instruction in a Dockerfile creates a new layer. A multi-stage build ensures that the final image is composed of a clean set of layers, making it easier to manage and cache.
    

---

#### How to Know What to Copy

The general rule is to copy the **dependencies** and the **application code**.

In the case of your Python app, the `pip install` command places all the installed libraries into a specific directory within the base image. You need to identify that location and copy it over to the final stage.

- The `RUN pip install` command in your `builder` stage places the packages in `/usr/local/lib/python3.10/site-packages`.
    
- The `COPY --from=builder /usr/local/lib/python3.10/site-packages /usr/local/lib/python3.10/site-packages` command simply moves that folder, with all its contents, to the same location in the smaller, final image.
    

The same logic applies to other languages. For example, with a Node.js app, you'd copy the `node_modules` folder. For a Go application, you would copy the single compiled binary file. You are essentially copying the "final product" from the build stage to the final stage.