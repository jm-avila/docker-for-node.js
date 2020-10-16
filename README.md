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

### Common Commands

**General:**

- docker --help
  - _Check the latest available commands on your Docker installation or on a specific command info of it's usage._
- docker version
  - _Provides docker version information._
- docker login
  - _Log in to a Docker registry._
- docker system prune
  - _Delete all unused containers, unused networks, and dangling images._

**Container:**

Use docker container my_command

- create
  - Create a container from an image.
- run
  - Create a new container and start it.
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
  - Start an existing container.
- stop
  - Gracefully stop running container.
- kill
  - Stop main process in container abruptly.
- restart
  - Stop and start a container.
- attach
  - Attach your local i/o stream to a running container.
- exec
  - Run a command in a active container.
- ls
  - List running containers.
- ps
  - Lists various properties of containers.
- inspect
  - See lots of info about a container.
- logs
  - Print logs.
- rm
  - Delete a stopped container.

**Images:**

Use docker image my_command

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

## Dockerfile

A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using docker build users can create an automated build that executes several command-line instructions in succession.

**Format**
INSTRUCTION arguments

e.g.

```
RUN echo 'we are running some # of cool things'
```

### Common Instructions

- FROM
- RUN
- WORKDIR
- COPY
- LABEL
- CMD

Note: Instructions order is very important because docker caches the layers and only rebuilds them from the layer that changed. Therefore it's best to first copy and install the dependencies and afterwards copy the source files, since the sources files change more often, making new builds will be faster as dependencies won't be rebuild if they haven't changed.
