
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
