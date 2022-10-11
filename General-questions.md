<br></br>
## Docker Basic concepts

### What is containerization ? 
Containerization is an approach to software development in which an application or service, its dependencies, and its configuration 
(abstracted as deployment manifest files) __are packaged together as a container image__.

### What is a virtual machine ?
Is a abstraction of an OS wich is created by a so-called `HyperVisor` - __physical hardware__. In windows the `Hyper-V` is used, and this one is exclusive for wirndows. 

### What is the difference between a virtual machine and a container ? 
Both give the required level of isolation that we need when deploying our applications, althgout the virtual machine 
is hardware resource expensive because it needs a __full-blow OS__ and so was consequence it also starts slow. 
With containers however the same OS of the host is shared across all the containers running on that machine, so we need only 
one OS license that we will update/patch and monitor. 

### What is a container ? 
An __isolated environment__ for running an application(or applications). A container is like a virtual machine in the sense that provides a isolated environment to run our applications. Can be stopped and restarted. Is just a OS process, but a special kind of process because it was is own File System.

### Why can i think of a container was instance of a process ?
Because just like a process a container does not maintain persistent state. However, we need to think of it was a `special process` that was is own File System.

### What is the advantages of containerization ? 
Containers offer the __benefits of isolation, portability, agility, scalability, and control__ across the whole application lifecycle workflow. 

### What is Docker ? 
Is a platform to build, deploy and run applications in a consisttent matter (across environemnts without `It works on my machine!`). 
> Docker is an open-source project for automating the deployment of applications as portable, self-sufficient containers that can run on the cloud or on-premises. Docker is also a company that promotes and improves this technology.

### What i need to run docker containers on my Windows development machine ? 
To host containers in development environments and provide additional developer tools, Docker offers `Docker Community Edition (CE)` for Windows. These product install the necessary VM (the Docker host) to host the containers.

### What are the two types of runtimes to run Windows Containers ? 
We have Windows Server Containers, they have isolation of each other throught process and namespace isolation (What is that ??). This type of containers share the Kernel with container host and with all the other containers running. Them we have Hyper-V containers they have better isolation because they run in a highly optimized virtual machine. In this case this type of containers do not share the Kernel with the Containers Host. The images for these containers are created the same way and function the same. The difference is in how the container is created from the image.

## What is a hypervisor ? 
Is software to create and manage virtual machines. For example : `VirtualBox`, `VMWare` and `Hyper-V` are examples of hypervisor software.  

### To conclude : 
#### Virtual Machines : 
- __Each VM needs a full-blow OS__ each needs to be licenced, updated and monitored.
- Is expensive in terms of Hardware.
- Is slow to start 

#### Container :
- Only requires a OS that needs to be licenced and monitor to patch/update when needed (containers share the same OS on the host)
- Is cheap in terms of Hardware.
- Is fast to start.

> Microsoft says : Virtual machines include the application, the required libraries or binaries, and a full guest operating system. Full virtualization requires more resources than containerization. Docker containers include the application and all its dependencies. On the other hand, they share the OS kernel with other containers, running as isolated processes in user space on the host operating system. (Except in Hyper-V containers, where each container runs inside of a special virtual machine per container proving more isolation)

### How is the Docker arquitecture ? 
The docker implements a client/server arquitecture, so there is a client and server wich is a Rest API. The server, also called __Docker Engine__ or __Daemon__ sits on the background building and running containers on a client request. Technically a `container` is a `process` just like any other, but is a __special kind of process__ is a __operating-sytem process with its own file system and other stuff (like network adapaters etc...).

### How the sharing of the OS works ?
The containers do not share all the OS, __they just share the Kernel__. The component of OS wich manages applications and hardware resources (is like the _motor in a car_). With that being said, `windows based containers` cannot run on linux was they need to talk to a Windows Kernel. Althgouth `Linux Containers` can run on Windows because on new versions of the windows there is actualy a custom build Linux Kernel (microsoft call it `WSDL - Windows Subsystem for Linux`). So, Linux containers running on Windows host shared this custom Linux Kernel and Windows Containers use the normal windows kernel that was always shipped with windows. What about Mac ? Mac kernel is very specific and __does not contain native support for containerezed applications__ so `Docker on Mac` uses a small Linux VM to run linux containers.

### What we need, to 'put' our application in a `Container` ? 
We need a `Docker File` that describes everthing the application needs to run (every dependencie etc...). Them __instead of directly launch the application and 
run it inside a process__ we tell docker to run it inside a container.

### What the Docker File does and how visual studio creates this file for me? 
Is a file wich allows us to config the container for our application such that the Docker knows how to set it up and run it. We can add "Docker support" in visual studio when starting a project checking the check box "Enable Docker support" or by right-clicking on the project and them : 
           
          Add > Docker Support.

### What is a `Dockarized` an application ? 
Is a application that was a `Docker File`. This `Docker File` is just a plain text file with all the instructions to run our application in a Docker Container. 
After adding the `Dockerfile` we dont need any deployment instructions files to deploy, we have the Docker file that describes everthing.

### What kind of processes the Containers can represent ? 
The container can represent long-term processe's like Web servers, or short-term processes like Batch jobs that we do with Scripts in Windows to them run them was windows services.

<br></br>
## Setting up Dockerfile and building images 

### Each commands i have in the docker file ? 
We have : 
- From : `Specify Base image. To start the container __From__ a basic __operation system base image__`
- Workdir : `To set a specific dir, after this command all follwing commands will be executed in that working dir.`
- COPY : `to copy files or directories`
- Add : `to add files or directories`
- Run : `to execute some OS commands (Linux or Windows)`
- Env : `to set a environment variable` 
- Expose : `to define the port where the container should run`
- User : `to choose each user account wiil run the application`
- Cmd : `To specify the command that should be executed when we start a container`
- Entrypoint : `To specify the command that should be executed when we start a container`

### What the field `ENTRYPOINT` does in the Docker file ? 
The `ENTRYPOINT` field allows us to configure a container that will run as an executable. The `ENTRYPOINT` defines the process whose lifetime controls the lifetime of the container. 

### What is the default Docker Host IP ? (pag. 91)
The default Docker Host IP is always 10.0.75.1

### How can i set up a container with powershell ? ( pag. 93)
Using Windows Container modules.

### What happens to the properties that i define in the `appsettings.json` when i use docker ? (pag. 109)
Those properties __will be overriden by the values of Environment Variables that are specify in docker-compose.override.yaml__ when we use docker.
In the docker-compose.yaml and docker-compose.override.yaml i can define those environment variables so that docker will set them was OS Environemnt Variables.
In my settings.json in the app : 
``` json
       { 
          "ConnectionString": "Server=tcp:127.0.0.1,5433;Initial Catalog=Microsoft.eShopOnContainers.Services.CatalogDb;User Id=sa;Password=[PLACEHOLDER]",      
          "ExternalCatalogBaseUrl": "http://localhost:5101",
           "Logging": 
           { 
              "IncludeScopes": false,
              "LogLevel": 
                { 
                  "Default": "Debug",
                  "System": "Information",
                  "Microsoft": "Information" 
                 } 
            } 
        }
```
In my docker-compose.override.yml file   
```yaml
 # docker-compose.override.yml 
 # 
    catalog-api: 
        environment: - ConnectionString=Server=sqldata;Database=Microsoft.eShopOnContainers.Services.CatalogDb;
    User Id=sa;Password=[PLACEHOLDER] 

    # Additional environment variables for this service. 
    ports: 
    - "5101:80"          
```
<br></br>

### What are the advantages of using the configuration in the docker-compose.yml files versus using configuration in files at the project or microservice level ?
The docker-compose.yaml files at the solution level are more flexible and secured than configuration files at project or microservice level. 

### How can i can I secure secret keys, like the connection string to my PRD SQL Server, cryptographic keys or API keys ? What products do you have in the market ?
For example, if we want to keep safe a connection string we can use the [Azure Key Vault](https://azure.microsoft.com/en-us/services/key-vault/). In local, 
there is some possibilities like keeping the keys in the User Home directory and so on...visual studio also now supports these kind of things.

## Containerizing monolithic applications

### If you have to create some application fast, like a POC application, what you would use ? Monolitic apporach or microservices ? (pag. 20)
I would use monolithic approach because the development is normally much easier. I dont have to worry about cross-cutting concerns in multiple applications, is much easier to debug and test. 

#### References : 
- https://www.n-ix.com/microservices-vs-monolith-which-architecture-best-choice-your-business/
    
### What is the problem of using containers for a big monolitic application ? 
When the application grows, some of his components are choke points and need to be scale. But all the rest not was is used less. So we wil scale horizontal, have multiple instances just because of some parts of the application, __wasting resources and time !__ . Also, is much more easy with microservices to split the work by teams than make everyone work in the same solution.
    
### Which products i can use from `Azure` to deploy my applications ? (pag.20)
We have `Azure Balancer` was a `Load Balancer` instead of F5. `Azure App Service` let's deploy applications in the cloud. 

#### References : 
- https://azure.microsoft.com/en-us/services/app-service/#overview ; https://docs.microsoft.com/en-us/azure/architecture/aws-professional/services
  
### How can i make the deployment of my application with Docker ? 
Deployment to our several hosts can be done using the traditional techniques. If we are using docker hosts can be managed with commands like 'docker run' or 'docker-compose' performed manually or thought automation with continuos delivery tools like `TeamCity` or `Jenkins`. Deployment of new versions of the application __using docker images is faster and network friendly__.    
To run our application in a Docker container we just need to do it like says [here](https://docs.docker.com/get-started/02_our_app/). In a pipeline is more complex.
   

  
<br></br>
## Docker and microservice arquitecture

### Is Docker necessary when building a microservice architecture? (pag. 94)
Docker provides a lot of benefits, however the use of docker is not a obligation. For example we can have a microservice arquitecture in `Azure Service Fabric` 
with each microservice running __was a single process without containers__. Otherwise we can use `Azure Service Fabric` with our microservices in Docker Containers.
Despite all this if you know how to use and deploy microservices based on containers you will know how to deploy more simple arquitecture based for example
in a single multi-tier application. 

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

<br></br>
## Working with Multi-container applications

### What a container orchestrator does ?   
Container orchestrators creates and manage the various intanstances that we need and also manages their lifetime.

### Why we need a docker-compose.yml file ?
We need it when we have a `multi-container application`. In the docker-compose.yml file we can define the set of related services/applications as a composed application using deployment commands. Configure all the dependencies of those services on each other and add run-time configuration. After we create that file we can run `docker-compose up --build` command against the `docker-compose.yml` file. This command will build all the related necessary images in __one go__. In such file we can find the name of the custom image for wich application and __configuration that might depend on the deployment environment__, like the connection string.

### What can we define for our multi-comainter application using the docker-compose file ? 
You would defined a so called multi-container deployment description where you can define each of the containers(with the applications) that should be deployed, and __how__ they should be deployed. Them, you can deploy the whole solution, everthing, with a single command by using the docker-compose up CLI command.

### How can we use the docker-compose files to target different environments ?
The docker-compose.yaml files are defintion files that can be interpreted by infracstructure(devOps) tools. The most typical one `docker-compose` command. We can use several docker-compose.yaml files to target multiple environments, having the configurations per environment. For example: `docker-compose.uat.yaml`, `docker-compose.prd.yaml` and we do `docker-compose [target-file]`.
    
### What is the difference between targeting Development, testing and production environments ?
In `Development` sometimes we need to run our application in some isolated, dedicated environment with new database, new redis etc... for that we can use docker-compose up command or use visual studio. For `Testing`, we need it when integration tests demand a fresh environment. For example, i want to test the Unique indexs in my database, i cannot do it with a in-memory database, so i do my integrations tests with the help of docker in a isolated environment. For `Production`, normally we __want to deploy to a REMOTE docker host__. Also, in case if we are using a Orchestrator we may need to add some more configuration and metadata files order than `docker-compose.yaml`.

<br></br>
## Orchestrate microservices and multi-container applications for high scalability and availability using (e.g.) Kubernets

### What is a orchestrator ? 
A orchestrator is a platform wich help us to scale out applications across many Docker hosts and managed them was single clusters (wich makes things much easier). Kubernetes is an example of an orchestrator, and is available in Azure through Azure Kubernetes Service.

### How to handle load-balancing, routing, and orchestrating for these composed applications? 
Well, the `docker engine` is perfectly capable of managing a couple of containers in a Host, however __it falls short when managing multiple cointainers in multiple hosts__. For those cases we need a management platform __that will start containers, scale out with multiple instances per image, restart or shutdown them down, and if possible controlling their acess to resources like storage and network__. These management platforms are called : orchestration and clustering platforms. These platforms help us to scale out applications across many Docker hosts and managed them was single clusters (wich makes things much easier). Kubernetes is an example of an orchestrator, and is available in Azure through `Azure Kubernetes Service`. These clusters can have Schedulling (most of them, like Kubernets do...) wich means the capability for an administrator to launch containers in a cluster. A cluster scheduller was several responsabilities : 
- Use the cluster's resources efficiently setting constratinst provided by the user (Memory usage, CPU usage etc...)
- `Efficiently load-balance` containers across nodes or hosts
- And to make sure the clusters are robust againts errors while providing High availability
Examples of such products : `Kubernets` ; `Azure Kubernetes Service`
      
### Can we use Docker engine to manage several containers deployed across many machines/hosts ?
Well, the docker engine is perfectly capable of managing a couple of containers in a Host, however it falls short when managing multiple cointainers in multiple hosts.
For that we should use a orchestrator like `Kubernets`.
    
### What are Helm Charts ? 
Is part of a production deployment strategy. For more simple applications when you want to deploy to Kubernets we can just use the CLI and a simple YAML file to define the configuration. However, in more complex microservice based-applications is recommended to use Helm charts. Because with Helm charts we can define, version, rollback, install, share and upgrade the most-complex applications. Some Kubernetes Azure services make use of Helm charts was well, for example `Azure Dev Spaces`.
      
### Why do we use Helm Charts ? 
We use Helm charts to easily define, version, install, share, rollback and upgrade the most complex kubernets based applications.
