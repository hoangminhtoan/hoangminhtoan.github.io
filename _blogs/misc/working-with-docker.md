---
layout: post
subtitle: Start Working with Docker
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
last_modified_at: 2020-08-28 17:58:00 +0000
tags: [docker]
---

## Table of Contents
* [Commands](*commands)
* [DockerFile](*dockerfile)


## Commands
* Install docker

* Create an image
```
docker build -t <repository>:<tag> .
```

* List all image
```
docker image ls
```




## Dockerfile
A Dockerfile is an automated way to build your Docker images.\
The Dockerfile contains special instructions, which tell the Docker Engine about the steps required to build an image.
```
FROM ubuntu:latest
LABEL author="<your name>"
LABEL description="<description of this image>"

ENV DEBIAN_FRONTEND=noninteractive

RUN mkdir /workspace
RUN mkdir /workspace/ml_with_cpp
RUN apt-get install python
```

### Commands in Dockerfile
* FROM\
Every valid Dockerfile must start with a **FROM** instruction.
```
FROM <image> [AS <name>]
or
FROM <image>[:<tag>] [AS <name>]
or
FROM <image>[@<digest>] [AS <name>]
```
Where ```<image>``` is the name of a valid Docker image from any public or private repository.

* WORKDIR
**WORKDIR** instruction sets the current working directory for **RUN, CMD, ENTRYPOINT, COPY** and **ADD** instructions.
```
WORKDIR /path/to/directory
```

* ADD and COPY\
These two instructions allow you to transfer files from the host to the containers filesystem.
 * COPY supports basic copyting of files to the container
 * ADD support for features like tarball auto extraction and remote URL support
```
ADD/COPY <source> <destination>
```
For Dockerfiles used to build Linux containers, both instructions allow you change the owner/group of the files being added to the container
```
ADD/COPY --chown=<user>:<group> <source> <destination>
```

* RUN\
The **RUN** instruction will execute any commands in a new layer on tops of current image and crate a new layer that is availabel for the next steps in the Dockerfile
```
RUN <command> (known as the shell form)
or
RUN ["executable", "param 1", "param 2"] (known as the exec form)
```
* CMD and ENTRYPOINT\
Define which command is executed when running a container.
```
CMD ["executable", "param 1", "param 2"] (known as the exec form)
or
CMD ["param 1", "param 2"] (as default parameters to ENTRYPOINT)
or
CMD <command> <param 1> <param 2> (shell form)

ENTRYPOINT ["executable", "param 1", "param 2"] (known as the exec form)
or
ENTRYPOINT <command> <param 1> <param 2> (shell form) 
```

