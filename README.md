# Docker for node.js

## Key Concepts

- docker host
- docker daemon
- docker client
- docker cli
- docker registry
- container
  - image
  - volume
  - networks

## Docker Host

Is a physical computer system or virtual machine running Linux. This can be your laptop, server or virtual machine in your data center, or computing resource provided by a cloud provider. The component on the host that does the work of building and running containers is the Docker Daemon.

## Docker Daemon

Is a persistent background process that manages the containers on a single host. It is a self-sufficient runtime that manages Docker objects such as images, containers, network, and storage.

## Docker client

The Docker client ( docker ) is the primary way that many Docker users interact with Docker. When you use commands such as docker run , the client sends these commands to dockerd , which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

## Docker CLI

The CLI uses the Docker REST API to control or interact with the Docker daemon through scripting or direct CLI commands.

## Docker Registry

The Registry is a stateless, highly scalable server side application that stores and lets you distribute Docker images. The Registry is open-source, under the permissive Apache license.

## Container

A container is simply another process on your machine that has been isolated from all other processes on the host machine. That isolation leverages kernel namespaces and cgroups, features that have been in Linux for a long time.

### Container Image

When running a container, it uses an isolated filesystem. This custom filesystem is provided by a container image. Since the image contains the container's filesystem, it must contain everything needed to run an application - all dependencies, configuration, scripts, binaries, etc. The image also contains other configuration for the container, such as environment variables, a default command to run, and other metadata.

### Container Volume

While containers can create, update, and delete files, those changes are lost when the container is removed and all changes are isolated to that container. With volumes, we can change all of this. Think of a volume as simply a bucket of data.

Volumes provide the ability to connect specific filesystem paths of the container back to the host machine. If a directory in the container is mounted, changes in that directory are also seen on the host machine. If we mount that same directory across container restarts, we'd see the same files.

There are three types of volumes:

- Named Volume
  Docker manages where on disk the volume is created, but you give it a volume name.
  Every time you use the volume, Docker will make sure the correct data is provided.
  Command e.g.
  ```
  docker volume create somevolumename
  docker run -v name:/path/in/container ...
  ```
- Anonymous Volume
  Docker handles where the files are stored. That fact makes it difficult, to refer to the same volume over time.
  Command e.g.
  ```
  docker run -v /path/in/container ...
  ```
- Host Volume
  Lives on the Docker host's filesystem and can be accessed from within the container. Command e.g.
  ```
  docker run -v /path/on/host:/path/in/container ...
  ```

## Container Network

One of the reasons Docker containers and services are so powerful is that you can connect them together, or connect them to non-Docker workloads.

Docker’s networking subsystem is pluggable, using drivers. Several drivers exist by default, and provide core networking functionality:

- bridge

  - The default network driver. Bridge networks are usually used when your applications run in standalone containers that need to communicate.
  - User-defined bridge networks are best when you need multiple containers to communicate on the same Docker host.

- host

  - For standalone containers, remove network isolation between the container and the Docker host, and use the host’s networking directly.
  - Host networks are best when the network stack should not be isolated from the Docker host, but you want other aspects of the container to be isolated.

### Common Commands

**Essential Management Commands:**

- Usage: docker command COMMAND
- Commands
  - container
  - image
  - volume
  - network
  - system

**General:**

Commands:

- docker --help
  - _Check the latest available commands on your Docker installation or on a specific command info of it's usage._
- docker version
  - _Provides docker version information._
- docker login
  - _Log in to a Docker registry._
- docker system prune
  - _Delete all unused containers, unused networks, and dangling images._

**container**
Usage: docker container COMMAND

Commands:

- create
  - _Create a container from an image._
- run
  - _Create a new container and start it._
  - -i
    - _short for --interactive. Keep STDIN open even if unattached._
  - -t
    - _short for --tty. Allocates a pseudo terminal that connects your terminal with the container’s STDIN and STDOUT._
  - -it
    - _By specifying both -i and -t you can interact with the container through your terminal shell._
  - -p
    - _short for --port. maps the container ports to your machine ports._
  - -e
    - _short for -env. Set environment variables._
  - v
    - _short for --volume. Bind mount a volume._
  - -rm
    - _Automatically delete the container when it stops running._
- start
  - _Start an existing container._
- stop
  - _Gracefully stop running container._
- kill
  - _Stop main process in container abruptly._
- restart
  - _Stop and start a container._
- attach
  - _Attach your local i/o stream to a running container._
- exec
  - _Run a command in a active container._
- ls
  - _List running containers._
- ps
  - _Lists various properties of containers._
- inspect
  - _See lots of info about a container._
- logs
  - _Print logs._
- rm
  - _Delete a stopped container._

**image**
Usage: docker image COMMAND

Commands:

- build
  - _Build an image._
- push
  - _Push an image to a remote registry._
- pull
  - _Pull an image from remote registry._
- ls
  - _List images._
- history
  - _See intermediate image info._
- inspect
  - _See info about an image, including the layers._
- rm
  - _Delete an image, can also be done with docker rmi._

**volume**
Usage: docker volume COMMAND

Commands:

- create
  - _Create a volume._
- inspect
  - _Display detailed information on one or more volumes._
- ls
  - _List volumes._
- prune
  - _Remove all unused local volumes._
- rm
  - _Remove one or more volumes._

**network**
Usage: docker network COMMAND

Commands:

- connect
  - _Connect a container to a network._
- create
  - _Create a network._
  - -d
    - _short for --driver. Driver to manage the Network (default "bridge")._
- disconnect
  - _Disconnect a container from a network._

**system**
Usage: docker system COMMAND

Commands:

- df
  - _Show docker disk usage._
- events
  - _Get real time events from the server._
- info
  _Display system-wide information._
- prune
  - _Remove unused data._

## Dockerfile

A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using docker build users can create an automated build that executes several command-line instructions in succession.

**Format**
INSTRUCTION arguments

e.g.

```
RUN echo 'we are running some # of cool things'
```

### Instructions

Instructions can be given in lowercase or uppercase letters. But to differentiate instructions and arguments, instructions are in uppercase.

```
# Comment
INSTRUCTION arguments
```

**Common Instructions**

- FROM
  - Is used to specify the image name, if it is not available locally it will be downloaded from docker hub registry.
- WORKDIR
  - Is used to set the working directory.
- ADD
  - Is used to copy files, directories and remote URL files to the destination within the filesystem of the Docker Images.
- COPY
  - Is used to copy files, directories and remote URL files to the destination within the filesystem of the Docker Images.
- LABEL
  - Is used to specify metadata informations to an image in key-value pairs.
- ENV
  -Is used to set environment variables with key and value. The variables will be set during the image build and are available after the container is launched.
- EXPOSE
  - Is used to inform about the network ports that the container listens on runtime.
- VOLUME
  - Is used to create or mount a volume to the docker container from the docker host filesystem.
- RUN
  - Is used to executes any commands on top of the current image.
- ENTRYPOINT
  - Is used to configure and run a container as an executable.
- CMD
  - Is used to set a command to be executed when running a container. There must be only one CMD in a Dockerfile. If more than one CMD is listed, only the last CMD takes effect.

Note: Instructions order is very important because docker caches the layers and only rebuilds them from the layer that changed. Therefore it's best to first copy and install the dependencies and afterwards copy the source files, since the sources files change more often, making new builds will be faster as dependencies won't be rebuild if they haven't changed.

## [.dockerignore file](https://docs.docker.com/engine/reference/builder/#dockerignore-file)

To use a file in the build context, the Dockerfile refers to the file specified in an instruction, for example, a COPY instruction. To increase the build’s performance, exclude files and directories by adding a .dockerignore file to the context directory.

This helps to avoid unnecessarily sending large or sensitive files and directories to the daemon and potentially adding them to images using ADD or COPY.

**Useful patterns**

- comment in dockerfile
  - ```
    # comment
    ```
- ignore git files
  - ```
    .git/
    .gitignore
    ```
- ignore contents of a directory but include the directory
  - ```
    directoryName/*
    ```
- recursively ignore all files of a specific type
  - ```
    **/*.extension
    ```
- include a specific file of the ignored type
  - ```
    **/*.extension
    !filename.extension
    ```
- the dockerfile works as a blacklist, ignoring all pattern matches but it can be inverted to work as a whitelist ignoring all files that don't match a pattern.
  - on line 1
    ```
      *
      !Dockerfile
    ```

## Docker Compose

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.

Compose works in all environments: production, staging, development, testing, as well as CI workflows.

Using Compose is basically a three-step process:

1. Define your app’s environment with a Dockerfile so it can be reproduced anywhere.

2. Define the services that make up your app in docker-compose.yml so they can be run together in an isolated environment.

3. Run docker-compose up and Compose starts and runs your entire app.

## docker-compose command

Define and run multi-container applications with Docker.

Usage:
docker-compose [-f <arg>...] [options] [--] [COMMAND] [ARGS...]
docker-compose -h|--help

Commands:

- build
  - _Build or rebuild services._
- create
  - _Create services._
- up
  - _Create and start containers._
- down
  - _Stop and remove containers, networks._
- restart
  - _Restart services._
- exec
  - _Execute a command in a running container._
- rm
  - _Remove stopped containers._
