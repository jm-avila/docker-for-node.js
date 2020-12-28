# CMD and ENTRYPOINT in Docker

Containers are not meant to host an operating system. Containers are meant to run a specific task or process such as to host an instance of a web server or application server or a database or simply to carry out some kind of computation or analysis. Once the task is complete the container exits the container only lives as long as the process inside it is alive.

If the process inside the container is stopped or crashes the container exits.

## Who defines what process is run within the container?

If you look at a docker file you will see an instruction called CMD which stands for command that defines the program that will be run within the container when it starts for the image.

For the nginx image it is the NGINX command. For the MySQL image it is the mysqld command.

## How do you specify a different command, from the one in the image Dockerfile, to start a container?

One option is to append a command to the docker run command and that way it overrides the default command specified within the image.

e.g.

```shell
docker run Ubuntu sleep 5
```

When the container starts, it runs the sleep program, waits for 5 seconds and then exits.

## How do you make that change permanent?

Create your own image from the base image and specify the new command at the Dockerfile.

There are two different ways of specifying the command.

1. command as is in a shell
2. JSON array format

e.g.

```yml
CMD sleep 5
CMD ["sleep", "5"]
```

When you specify in a JSON array format, the first element in the array should be the executable the second the parameter.

## What if I wish to change the number of seconds it sleeps currently?

One option is to run the docker run command with the new command appended to it.

e.g.

```shell
docker run "new_image_name" sleep 10
```

A second options is using the ENTRYPOINT instruction. With it we could only pass the number of seconds to the container, and the sleep command would be invoked automatically.

The ENTRYPOINT instruction is like the CMD instruction as in you can specify the program that will be run when the container starts and whatever you specify on the command line.

Dockerfile e.g.

```yml
ENTRYPOINT ["sleep"]
```

CLI e.g.

```shell
docker run "new_image_name" 10
```

In case of the CMD instruction the command line parameters passed will get replaced entirely whereas in case of ENTRYPOINT the command line parameters will get appended.

## How do you configure a default value for a command?

You would use both ENTRYPOINT as well as the CMD instruction.

Dockerfile e.g.

```yml
ENTRYPOINT ["sleep"]
CMD ["5"]
```

In this case the CMD instruction will be appended to the ENTRYPOINT instruction. If you specify any parameters in the command line then that will override the CMD instruction.

For this to happen you should always specify the ENTRYPOINT and CMD instructions in a JSON format.

## What if you feel you really want to modify the ENTRYPOINT during runtime?

You can override it by using the entrypoint option in the docker run command.

CLI e.g.

```shell
docker run --entrypoint ls "image_name" .
```
