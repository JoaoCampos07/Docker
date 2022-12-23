
# Dockerfile instructions : 

``` powershell
FROM         # to specify the base image
WORKDIR      # to set the working directory
COPY         # to copy files/directories
ADD          # to copy files/directories
RUN          # to run commands
ENV          # to set environment variables
EXPOSE       # to document the port the container is listening on
USER         # to set the user running the app
CMD          # to set the default command/program
ENTRYPOINT   # to set the default command/program
```
------
# Docker Commands 
## Image Commands : 
``` powershell
docker build -t <name> .
docker images
docker image ls
docker run -it <image> sh
```

## Starting and Stopping containers :
``` powershell
docker stop <containerID>
docker start <containerID>
```
## Executing commands in running containers :
``` powershell
# the difference betwen `docker run` and `docker exec` is that `docker run` is to
# run containers and `docker exec` is to execute a command in a already running
# container

docker exec c1 ls

docker exec -it c1 sh # let's open a shell
```

## Removing Containers 
``` powershell
docker container rm <containerID>
docker rm <containerID>
docker rm -f <containerID>        # to force the removal
docker container prune            # to remove stopped containers
```

## Volumes 
``` powershell
docker volume ls
docker volume create app-data
docker volume inspect app-data
docker run -v app-data:/app/data <image>
```

## Copying files between the host and containers 
``` powershell
docker cp <containerID>:/app/log.txt .
docker cp secret.txt <containerID>:/app
```

## Sharing source code with containers 
``` powershell
docker run -v $(pwd):/app <image>
``` 

## Clean our Workspace : 
### 1. Remove all containers (before images) : 
``` powershell
docker container rm -f $(docker container ls -a -q)
```
### 2. Remove all images : 
``` powershell
docker image rm $(docker image ls -q)
```

## Questions : 
### If i build some image and them i need to make changes, how i avoid creating new image ? How can i overide existing image ?
