# Enviorment Variables

It is a best practice to move some variables values out of the application code and into say an environment variable. Some values can change over time and shouldn't affect the code, some are confidential and can't be part of the source code.

## -e option

To pass the environment variable when running a container use the -e option.

e.g.

```shell
docker run -e "variable name"="variable value" "image name"
```

## How do we find the environment variable set on a container that's already running?

Use the docker inspect command to inspect the properties of a running container. Under the config section you will find the list of environment variables set on the container.
