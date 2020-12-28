# docker run

## tags

By default the docker run command runs the latest available version of an image. To run another version, for example an older version. You specify the version separated by a colon. This is called a tag.

e.g.

```shell
docker run redis:4.0
```

## Standard Streams

_STDIN, STDOUT, STDERR: In computer programming, standard streams are preconnected input and output communication channels between a computer program and its environment when it begins execution. The three input/output (I/O) connections are called standard input (stdin), standard output (stdout) and standard error (stderr)._

### -i option (stdin)

Given a simple prompt application that when run asks for name and on entering a name prints a welcome message. If I were to dockerize this application and run it as a docker container, it wouldn’t wait for the prompt. It just prints whatever the application is supposed to print on standard out.

That is because by default the docker container does not listen to a standard input. Even though you're attached to its console it is not able to read any input from you. It doesn't have a terminal to read inputs from. It runs in a non interactive mode.

To provide your input, you must map the standard input of your host to the docker container using the -i option. -i is for interactive mode.

When I input my name it prints the expected output. But before dockerized it asked us for our name, and when dockerized that prompt is missing.

With the interactive mode the app accepted the input and prompted on the terminal, but we have not attached to the containers terminal.

## –t option (stdout)

The –t stands for psueod terminal. With this option we can attach to the containers terminal.

With the combination of -i and -t we can now attach to the terminal as well as in an interactive mode on the container.

## –p option

Port mapping or port publishing on containers.

Imagine a simple web application in a docker container on your Docker host. Remember the underlying host where Docker is installed is called Docker host or Docker engine. When we run a containerized web application it runs and we are able to see that the server is running.

How does a user access my application?

Although the application is listening on port 5000, what IP do I use to access it from a web browser?

Use the IP of the docker container, every docker container gets an IP assigned by default. But remember that the internal IP is only accessible within the container host, users outside of the container host cannot access the app using this IP.

So we have an IP address for the docker container, available from inside of the container, and an IP address for the docker host available from outside the container.

To access the app using the docker host IP address we first need to map the port inside the docker container to one of the docker host free ports.

e.g.

```shell
docker run -p "docker host PORT":"container PORT" "image name"
```

For example, if I want the users to access my application through port 80 on my Docker host, I could map port 80 of local host to port 5000 on the docker container using the -p option in my run command.

e.g.

```shell
docker run -p 80:5000 user/myServer
```

This way you can run multiple instances of your application and map them to different ports on the docker host or on instances of different applications on different ports.

## –v option

How is data persisted in the docker container? The docker container has its own isolated file system and any changes to any files happen within the container.

What happens if you were to delete the mysql container and remove it?

As soon as you do that the container along with all the data inside it gets blown away and meani all your data is gone.

If you want to persist data, you need to map a directory on the container host, to a directory from the Docker host inside the container.

e.g.

```shell
docker run -v "container host path":"docker host path" "image name"
```

This way when docker container runs it will implicitly mount the external directory to a folder inside the docker container. This way all your data will now be stored in the external volume at the choosen path and thus will remain even if you delete the docker container.

## docker inspect

The docker ps command is good enough to get basic details about containers but if you want to see additional details about a specific container use the docker inspect command and provide the container name or I.D. It returns all details of a container in a JSON format.

## docker logs

How do we see the logs of a container we ran in the background?

Specify the container I.D. or name.

For example I ran my simple web application using the -d parameter and it ran the container in a detached mode. How do I view the logs which happens to be the contents written to the standard out of that container.
