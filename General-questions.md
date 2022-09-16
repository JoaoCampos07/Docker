### What is containerization ? 
Containerization is an approach to software development in which an application or service, its dependencies, and its configuration 
(abstracted as deployment manifest files) are packaged together __as a container image__.

### What is a container ? 
An __isolated environment__ for running an application(or applications).

### What is the advantages of containerization ? 
Containers offer the __benefits of isolation, portability, agility, scalability, and control__ across the whole application lifecycle workflow. 

### What is Docker ? 
Is a platform to build, deploy and run applications in a consisttent matter (across environemnts withou `It works on my machine!`). 
> Docker is an open-source project for automating the deployment of applications as portable, self-sufficient containers that can run on the cloud or on-premises. Docker is also a company that promotes and evolves this technology.

### What i need to run docker containers on my Windows development machine ? 
To host containers in development environments and provide additional developer tools, Docker ships Docker Community Edition (CE) for Windows. These products install the necessary VM (the Docker host) to host the containers.

### What are the two types of runtimes to run Windows Containers ? 
We have Windows Server Containers, they have isolation of each other throught process and namespace isolation (What is that ??). This type of containers share the Kernel with container host and with all the other containers running. Them we have Hyper-V containers they have better isolation because they run in a highly optimized virtual machine. In this case this type of containers do not share the Kernel with the Containers Host. The images for these containers are created the same way and function the same. The difference is in how the container is created from the image.

### What is the difference between virtual machines and docker containers ? 

### What is a virtual machine ?
Is a abstraction of an OS wich is created by a so-called `HyperVisor` - __physical hardware__. In windows the `Hyper-V` is used, and this one is exclusive for wirndows. 

## What is a hypervisor ? 
Is software to create and manage virtual machines. For example : `VirtualBox`, `VMWare` and `Hyper-V`.  

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

### What the Docker File do and how visual studio creates this file for me? (pag. 77, pag.79)
Is a file wich allows us to config the container for our application such that the Docker knows how to set it up and run it. We can add "Docker support" in visual studio when starting a project checking the check box "Enable Docker support" or by right-clicking on the project and them : 
           
          Add > Docker Support.

### What is `Dockarized` an application ? 
We make a small change in our application. We add a `Docker File`, a plain text file with all the instructions to run our application in a Docker Container. 
So, after docker we dont need deploy instructions files to deploy we have the Docker file that describes everthing.

### What the field `ENTRYPOINT` does in the Docker file ? 
The `ENTRYPOINT` field allows us to configure a container that will run as an executable. The `ENTRYPOINT` defines the process whose lifetime controls the lifetime of the container. 
     
### What kind of processes the Containers can represent ? 
The container can represent long-term processe's like Web servers, or short-term processes like Batch jobs that we do with Scripts in Windows to them run them was services.

<br></br>
## Containerizing monolithic applications

### If you have to create some application fast, like a POC application, what you would use ? Monolitic apporach or microservices ? (pag. 20)
I would use monolithic approach because the development is normally much easier. I dont have to worry about cross-cutting converns in multiple applications, is much easier to debug and test and also is simple to deploy. 

#### References : 
- https://www.n-ix.com/microservices-vs-monolith-which-architecture-best-choice-your-business/
    
### What is the problem of using containers for a big monolitch application ? 
When the application grows, some of his components are choke points and need to be scale. But all the rest not was is used less. So we wil scale horizontal, have multiple instances just because of some parts of the application, __wasting resources and time !__ . Also, is much more easy with microservices to split the work by teams than make everyone work in the same solution.
    
### Which products i can use from `Azure` to deploy my applications ? (pag.20)
We have `Azure Balancer` was a `Load Balancer` instead of F5. `Azure App Service` let's deploy applications in the cloud. 

#### References : 
- https://azure.microsoft.com/en-us/services/app-service/#overview ; https://docs.microsoft.com/en-us/azure/architecture/aws-professional/services
  
### How can i make the deployment of my application with Docker ? 
Deployment to our several hosts can be done using the traditional techniques. If we are using docker hosts can be managed with commands like 'docker run' or 'docker-compose' performed manually or thought automation such as continuos delivery using `TeamCity` or `Jenkins`. Deployment of new versions of the application __using docker images is faster and network friendly__.    
To just run our application in a Docker container we just need to do like says [here](https://docs.docker.com/get-started/02_our_app/). In a pipeline is more complex.
   
### What a container orchestrator does ?   
Container orchestrators creates and manage the various intanstances that need and also manages their lifetime.
  
### Why can i think of a container was instance of a process ?
Because just like a process a container does not maintain persistent state. However, we need to think of it was a `special process` that was is own File System.

<br></br>
## State and data in Docker applications

### What are the solutions for managing Data in Docker applications ? 
Volumes, Bind Mounts, tmpfs mounts our Remote storage, using `Azure Store` or Remote Relational Databases (RBMS).
   
### When use Docker Volumes where the data in stored in filesystem ? 
Is stored in a area (directory or disk) that's managed by Docker. 
  
### What is the security problem with Bind Mounts ?
Bind mounts can map to any folder in the host filesystem, allowing the container to write or read to virtually any place. And maybe some directory was sensitive information and should not be accessed by some users.
  
### What are tmpfs mounts ? 
Are like virtual folders inside the host memory that are never really created in the filesystem, they just exist in dynamic memory.
   
### How can i share data between containers that live in different hosts ? 
I can use Redis, SQL Databases or Non-SQL databases. We can also use a remote driver that supports remote hosts.
   
### Why i should not use data volumes for business data ? 
The data volumes are shared between the containers and the containers can "move" between hosts, so we may end up losing business data because some microserivce did not had the access to the data volume that we expected. 
