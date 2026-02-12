Dockerfile is a text-file that is used to create Docker images. Its advantages can be seen [[Docker Management#^134809|here]].

To create one, just create a file named "Dockerfile". Here is the text:

```
FROM ubuntu

# Skip prompts (like the tzdata location)
ARG DEBIAN_FRONTEND=noninteractive

# Update packages
RUN apt update; apt dist-upgrade -y

# Install packages
RUN apt install -y apache2 curl

# Set entrypoint
ENTRYPOINT ["apache2ctl", "-D", "FOREGROUND"]


```



To create a container from the image, you should run 
- `docker build -t atakan/apache-test:1.2 .`

To run a custom image:
- `docker run -p 3000:3000 apache-test`

## Creating Images

In the application development directory, you will create a Dockerfile. It should be in the same directory, since you will be copying your files into the image.
#### FROM
When creating Docker images for your application, you need to first determine a **base image**. It is used to put everything on top.
```
FROM node:19-alpine
```

> You can use `AS` tag, like "AS builder" for multi-stage builds 
#### WORKDIR
Another command is WORKDIR. When you copy your code into a specific folder in the container image, you should actually be running commands there.

```
WORKDIR /app
```

#### COPY
Then, you should copy your actual code and config files with COPY. It copies the config and development files THAT IS ON YOUR COMPUTER to the IMAGE when you are creating. It also creates directories if not exist.

```
COPY package.json /app
COPY programming_files /app
```

#### RUN
This command is used to run actual commands, like installing dependencies that exist in a package.json file in this example

```
RUN npm install
```
#### CMD
This command is used for the instructions. This is used as the last command on the Dockerfile, and there can **only be 1 CMD command**.

```
CMD ["node", "server.js"]
```

#### Environmental Variables
You can specify environmental variables like this. Although it is suggested to define them externally, either in docker command or compose file so you can just change it easily with a restart instead of a full image build

```
ENV MONGO_DB_USERNAME=admin
```

Expose??
#### EXPOSE
It is for explanation. It tells the user that "this app uses this port". 
Also, when you use -P instead of -p, it can bind a high numbered random port to the port of EXPOSE
```
EXPOSE 5000
```