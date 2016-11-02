**Docker Reference**

Docker consists of a client and a server that communicate over a socket.

When installed on Windows/Mac OSX, Docker now has solutions that run without requiring a VM. However, docker-machine, an older solution that requires a VM is  still available.

If you want to use docker-machine:


Once you install docker, create the default instance of the VM using:

```
docker-machine create --driver hyperv default
```

> the vm should be known as `default`.

To connect to the vm once we have created it:

```
docker-machine ssh
```

> this downloads the `boot2docker` image and installs it on Oracle Virtualbox

To get docker to talk to your new machine:

```
eval "$(docker-machine env default)"
```

on bash but you need to set the environment variables manually in Windows.

Working with the VM:

+ docker-machine start

+ docker-machine stop

+ docker-machine restart

+ docker-machine upgrade

+ docker-machine kill

+ docker-machine ip

+ docker-machine inspect

---

A `Docker image` is a barebones version of an OS to perform certain core functionalities.

An image can be used to create containers, a container cannot affect the image it was created from.

Running bash in an ubuntu container with an interactive terminal environment:

```
docker run -ti ubuntu:14.04 bash
```

You can add the `rm` flag to tell a container to remove itself once it is done.

```
docker run -ti --rm ubuntu:14.04 bash
```

To create a new image from an existing image:

```
docker tag <imageId> imageName:tagName
```

When creating containers, it is a good practice to prefix it with the organisation name like `orgname/imagename`. If no tag name is specifed, docker fills in the tagName `latest`.

To create an image with a container and tag it:

```
docker commit containerId imageName:tagName
```

To remove an image:

```
docker rmi imageName:tagName
```

To start from a container:

```
docker start containerName
```

To attach to a container:

```
docker attach containerName
```

To kill a container:

```
docker kill containerName
```

To remove a container:

```
docker rm containerName
```

If you pass `rm` flag into the container configuration, it will be removed once you kill it.

There are other options to limit the resources that a container can use for `docker run`

+ `--memory-allowed-maximum`

+ `--cpu-shares`

+ `--cpu-quota`

**Networking**

To see all the exposed ports on all the containers:

```
docker port containerName
```

To expose a port on a container dynamically:


```
docker run -ti --rm -p portName ubuntu:latest bash
```

To expose a port on container:

```
docker run -ti --rm -p hostPort:containerPort ubuntu:latest bash
```

By default, the container expects that we are using a tcp port within the container. If we want to expose a port using `udp` we need to use the full command:


```
docker run -ti --rm -p hostPort:containerPort/protocol ubuntu:latest bash
```

We can link containers directly:

```
docker run -ti --rm --link serverContainer --name clientContainer
```

---

To create connections between two or more containers, docker uses private networks. To list all networks:

```
docker network ls
```

To create a private network:

```
docker network create my-network
```

To create containers connected to a network:

```
docker run -ti --rm --name client1 --network networkName ubuntu bash
docker run -ti --rm --name client2 --network networkName ubuntu bash
```

To inspect a network:

```
docker network inspect networkName
```

All clients connected to a network can talk to each other. You can restart a container and the other containers will still be able to talk to the container on the new IP address.

To remove a network:

```
docker network rm networkName
```

---

**I/O**

There are two kinds of volumes:

1. shared-volume

2. ephemeral

A shared volume exists on the host and is shared with the container. When we want to share a container with the rest of the world, avoid shared volumes.

An ephemeral volume exists on the container, it is destroyed when no container is using them. Ephemeral volumes can be shared between containers

> I cannot see shared volumes between host and container in windows

To create a shared-volume use:

```
docker run -ti  -v hostPath:containerPath ubuntu latest
```

To create a ephemeral volume use:

```
docker run -ti -v containerPath ubuntu latest
```

To use the ephemeral volume in another container:

```
docker run -ti --volumes-from containerPath ubuntu latest
```
---

**Creating and sharing images using `Dockerfile`**

This is a simple Dockerfile:

```
FROM busybox
#runs in an intermediate container
RUN echo "building a simple container"
#runs when the container starts
CMD echo "hello container"
```

To build the dockerfile use:

```
docker build .
```

Then tag the image:

```
docker tag containerId imageName
```

A Dockerfile is built line by line, each line creates a container and an image is built based on the container. This image becomes the base image from which the container on the next line is built.

Docker is memory effecient and shares memory between these intermediate images.

+ `FROM` is to use a reference image that you want to use build your image

> usually we use one image and we place the `FROM` at the top of the `Dockerfile`

+ `MAINTAINER` is used to specify the name of the maintainer(that's you/me??)

+ `RUN` runs a command in a shell and saves the result

+ `ADD` can be used to add `local files`,`archives` and `urls` to the container.

+ `ENV` sets environment variables that can be used in the Dockerfile and in the container.

> When a container runs, we either use `ENTRYPOINT` or `CMD`.

+ `ENTRYPOINT` is used when we know which command should run and only want to allow arguments to be passed to the command.

+ `CMD` is used when we want to specify a command but allow the user to replace it with a command of their own choice if needed.

+ `EXPOSE` exposes a port on the container

+ `VOLUME` can create either a shared volume or an ephemeral volume, in order to create a shared volume, you need to provide two arguments:

```
VOLUME ["hostPath","containerPath"]
```

> The above format `[]` can be used with `CMD` as well, this is known as the `CMD` form while just specifying a command is known as the `shell form`.

+ `WORKDIR` sets the working directory for the rest of the container and for the container to run `CMD` in.

+ `USER` sets the user that the command should run as.

---