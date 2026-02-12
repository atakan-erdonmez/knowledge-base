In order to use private repo, you need to create one in a system.

1- Login
`docker login`
2- Tag
`docker tag <this_name> <to_this_name>
2- Push
`docker push repo_url/my-app:3.1`


#### Image Naming
registryDomain/imageName:tag


The full path of DockerHub images are:
- docker.io/library/mongo:4.2

# Setting up a Private Registry
I will use the open-source Docker [registry](https://hub.docker.com/_/registry) container. 

## Basic commands

Start your registry
```sh
docker run -d -p 5000:5000 --name registry registry:3
```

Pull (or build) some image from the hub
```sh
docker pull ubuntu
```

Tag the image so that it points to your registry
```sh
docker image tag ubuntu localhost:5000/myfirstimage
```

Push it
```sh
docker push localhost:5000/myfirstimage
```

Pull it back
```sh
docker pull localhost:5000/myfirstimage
```

Now stop your registry and remove all data
```sh
docker container stop registry && docker container rm -v registry
```

To mount a volume
```
-v /mnt/registry:/var/lib/registry
```


### Interaction with Registry

localhost:5000/v2/\_catalog -> check images 