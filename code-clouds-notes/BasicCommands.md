# Basic Commands

## docker run

Used to run a container from an image.

e.g.

```shell
docker run nginx
```

This will run an instance of the nginx application on the docker host. If the image is not present on the host it will go to docker hub and pull that image down.

## docker ps

Lists all running containers and some basic information about them such as:

- Container I.D.
- Image name
- Current status
- Container name

### -a option

See all containers, running, previously stopped or exited containers.

## docker stop

Stop a running container, you must provide either the container I.D. or name.

## docker rm

Remove a stopped or exited container permanently.

## docker images

List images.

## docker rmi

Remove image. _You must stop and delete all dependent containers to be able to delete an image._

## docker pull

Download an image without running it.

## docker run “image” sleep “number”

When the container starts it runs to sleep command and goes into sleep for a “number” of seconds.

## docker exec

Execute a command on a running docker container.

e.g.

```shell
docker exec “container name” cat “path”
```

Print the contents of the file at “path”

If you run a container, like a simple web server. It will run in the foreground or in an attached mode meaning you will be attached to the console or the standard out of the docker container and you will see the output of the web service on your screen. You won't be able to do anything else on that console other than view the output until this docker container stops. To stop the container press the CTRL + C combination.

### -d option

The docker container will run in detached mode. This will run the docker container in the background mode and you will be back to your terminal prompt immediately.

e.g.

```shell
docker run -d “image”
```

## docker attach

Attach a running container console or the standard out to your host console, by specifying the name or I.D. of the container.

When you're specifying the I.D. of a container in any Docker command you can simply provide the first few characters alone just so it is different from the other container I.D. on the host.
