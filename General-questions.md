### What is containerization ? 
Containerization is an approach to software development in which an application or service, its dependencies, and its configuration 
(abstracted as deployment manifest files) are packaged together __as a container image__.

### What is the advantages of containerization ? 
Containers offer the __benefits of isolation, portability, agility, scalability, and control__ across the whole application lifecycle workflow. 

### What is Docker ? 
Is a platform to build, deploy and run applications in a consisttent matter (across environemnts withou `It works on my machine!`). 
> Docker is an open-source project for automating the deployment of applications as portable, self-sufficient containers that can run on the cloud or on-premises. Docker is also a company that promotes and evolves this technology.

### Can windows images run on Linux at the time of this writing ? 
No, Windows images can run only on Windows Hosts and Linux images can run only on Windows (using a Hyper-V linux VM) or Linux hosts. Where host means a server or a VM.

### What i need to run docker containers on my Windows development machine ? 
To host containers in development environments and provide additional developer tools, Docker ships Docker Community Edition (CE) for Windows. These products install the necessary VM (the Docker host) to host the containers.

### What are the two types of runtimes to run Windows Containers ? 
We have Windows Server Containers, they have isolation of each other throught process and namespace isolation (What is that ??). This type of containers share the Kernel with container host and with all the other containers running. Them we have Hyper-V containers they have better isolation because they run in a highly optimized virtual machine. In this case this type of containers do not share the Kernel with the Containers Host. The images for these containers are created the same way and function the same. The difference is in how the container is created from the image.

### What is the difference between virtual machines and docker containers ? 

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

> Microsoft response : Virtual machines include the application, the required libraries or binaries, and a full guest operating system. Full virtualization requires more resources than containerization. Docker containers include the application and all its dependencies. On the other hand, they share the OS kernel with other containers, running as isolated processes in user space on the host operating system. (Except in Hyper-V containers, where each container runs inside of a special virtual machine per container.)

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
