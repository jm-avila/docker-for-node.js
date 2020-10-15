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
