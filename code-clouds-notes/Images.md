# Images

## How do you create your own image?

First we need to understand what we are containerizing or what application we are creating an image for and how the application is built.

## Dockerfile

Dockerfile is a text file written in a specific format that Docker can understand.

It's in an instruction and arguments format.

Everything on the left in CAPS is an instruction. Each instruct Docker to perform a specific action while creating the image.

Everything on the right is an argument to those instructions.

Every Docker image must be based off of another image.

Either an OS or another image that was created before based on an OS.

You can find official releases of all operating systems on Docker Hub.

It's important to note that all Docker files must start with a from instruction.

The run instruction instructs Docker to run a particular command on those base images.

When Docker builds the images it builds these in a layered architecture.

Each line of instruction creates a new layer in the docker image with just the changes from the previous layer.

Since each layer only stores the changes from the previous layer it is reflected in the size as well.

## docker history

You could see this information if you run the docker history command followed by the image name when you run the docker build command.

You could see the various steps involved and the result of each task.

All the layers build are cached so the layered architecture helps you restart docker build from that particular step in case it fails or if you were to add new steps in the build process you wouldn't have to start all over again.

All the layers built are cached by Docker so in case a particular step was to fail and you work to fix the issue and re-run docker build it will re-use the previous layers from cache and continue to build the remaining layers.

The same is true if you were to add additional steps in the docker file this way rebuilding your image is faster and you don't have to wait for a docker to rebuilt the entire image each time.

This is helpful especially when you update source code of your application as it may change more frequently only the layers above the updated layers needs to be rebuild.

A number of products are containerized such as databases, development tools, operating systemsm, etc. But that's just not it.

You can containerized almost all of the application even simple ones like browsers or utilities like curl, applications like Spotify, Skype, etc. Basically you can containerize everything.

## docker build

First create a docker file named Dockerfile and write down the instructions for setting up your application in it such as installing dependencies, where to copy the source code from and to and what the entry point of the application is, etc.

e.g.

```shell
docker build -t "continaer name" "docker file path"
```

This will create an image locally on your system.

## docker push

To local images available on the public Docker Hub registry run the docker push command and specify the name of the image you created.

```shell
docker push "image name"
```
