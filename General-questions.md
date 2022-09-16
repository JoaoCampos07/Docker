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
Virtual machines include the application, the required libraries or binaries, and a full guest operating system. Full virtualization requires more resources than containerization. Docker containers include the application and all its dependencies. On the other hand, they share the OS kernel with other containers, running as isolated processes in user space on the host operating system. (Except in Hyper-V containers, where each container runs inside of a special virtual machine per container.)
