
## Introduction to Docker 
### What is docker ? 
Is a platform to build, deploy and run applications in a consisttent matter (across environemnts withou `It works on my machine!`). 

### What is a virtual machine ?
Is a abstraction of an OS wich is created by a so-called `HyperVisor` - __physical hardware__. In windows the `Hyper-V` is used, and this one is exclusive for wirndows. 

## What is a hypervisor ? 
Is software to create and manage virtual machines. For example : `VirtualBox`, `VMWare` and `Hyper-V`.  

### What is a container ? 
An __isolated environment__ for running an application(or applications). 

### What is the difference between a virtual machine and a container ? 
Both give the required level of isolation that we need when deploying our applications, althgout the virtual machine 
is hardware resource expensive because it needs a __full-blow OS__ and so was consequence it also starts slow. 
With containers however the same OS of the host is shared across all the containers running on that machine, so we need only 
one OS license that we will update/patch and monitor. 

To conclude : 
#### Virtual Machines : 
- __Each VM needs a full-blow OS__ each needs to be licenced, updated and monitored.
- Is hardware resource expensive
- Is slow to start 

#### Container :
- Only requires a OS that needs to be licenced and we patch/update, monitor (containers share the same OS on the host)
- Need less hardware resource expensive
- Is fast to start.

### How is the Docker arquitecture ? 
The docker implements a client/server arquitecture so there is a client and server wich is a Rest API. The server, also called __Docker Engine__ or __Daemon__ sits on the background
building and running containers. Technicall a `container` is a `process` just like any other, but is a __special kind of process__ is a __operating-sytem process with its own file system and other stuff (like network adapaters etc...).

### How the sharing of the OS works ?
The containers do not share all the OS, they actually share the Kernel. The component of OS wich manages applications and hardware resources (is like the _motor in a car_).
With that being said, `windows based containers` cannot run on linux was they need to talk to a Windows Kernel. Althgouth `Linux Containers` can run on Windows because 
on new versions of the windows there is actualy a custom build Linux Kernel (microsoft call it `WSDL - Windows Subsystem for Linux`). So, Linux containers running on Windows host shared this custom Linux Kernel 
and Windows Containers use the normal windows kernel that was always shipped with windows. What about Mac ? Mac kernel is very specific and __does not contain native support for containerez applications__ so `Docker on Mac` uses a small Linux VM to run linux containers.

### What we need to put our application in a `Container` ? 
We need a `Docker File` that describes everthing a application needs to run (every dependencie etc...). Them __instead of directly launch the application and 
run it inside a process__ we tell docker to run it inside a container.

### What is `Dockarized` an application ? 
We make a small change in our application. We add a `Docker File`, a plain text file with all the instructions to run our application in a Docker Container. 
So, after docker we dont need deploy instructions files to deploy we have the Docker file that describes everthing.

## The Linux Command Line  
### Let's start by running a docker container interactively : 
``` powershell
docker pull ubuntu 
# OR 
docker run ubuntu
# Like that will search for this image locally and if it does not find it
# will pull it from the internet
```
Them we have :
``` powershell
PS C:\Users\joaoc> docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
405f018f9d1d: Pull complete
Digest: sha256:b6b83d3c331794420340093eb706a6f152d9c1fa51b262d9bf34594887c2c7ac
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```
When we do `docker run` the container just build, runs and shutsdown. So we need to build it interactively :
``` powershell
PS C:\Users\joaoc> docker run ubuntu
PS C:\Users\joaoc> docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
PS C:\Users\joaoc> docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS                     PORTS     NAMES
4d9397cd0bf1   ubuntu         "bash"                   9 seconds ago   Exited (0) 8 seconds ago             sleepy_blackwell
f1b140cdc82b   hello-docker   "docker-entrypoint.s…"   22 hours ago    Exited (0) 22 hours ago              zealous_galois
```
![image](https://user-images.githubusercontent.com/49458268/180814044-e03a07e1-0f42-47b0-97b2-037ed0d2b27b.png)

What `root@7e01079dc012:/#` stands for ? 
- root : the name of the user. The `root` user in this case is the most priviliged user.
- @ :
- 7e01079dc012 : 
- / : We are in the highest directory of the file system inside the container
- # : It means i have all the priviligies. Instead of `#` i could have `$`.

## Why the container just shutsdown when we do `docker run [image]` ?
Is like this by default, if we dont interact with it, it just shutsdown.
