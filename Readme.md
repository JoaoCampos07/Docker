
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

# Dealing with Images : 

## Putting some image on my public docker hub
``` powershell

docker images
REPOSITORY                         TAG                IMAGE ID       CREATED       SIZE
# I want to tag this bad boy here
jenkins-agent-dotnet-with-server   latest             00c129889651   2 hours ago   896MB

docker image tag e3e joaocampos07/jenkins-agent-with-dotnet:v1

# Let's login to push this image
docker login

# Check the images one last time
docker images
REPOSITORY                               TAG                IMAGE ID       CREATED       SIZE
joaocampos07/jenkins-agent-with-dotnet   v1                 e3e25a0dbcf2   6 days ago    896MB
jenkins-agent-dotnet                     latest             e3e25a0dbcf2   6 days ago    896MB

# push it to repo 
docker push joaocampos07/jenkins-agent-with-dotnet:v1
````

## Starting and Stopping containers :
``` powershell
docker stop <containerID>
docker start <containerID>

# e.g. :
docker run ubuntu # since we are not interacting with the container it will finish
docker run -it ubuntu 
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
