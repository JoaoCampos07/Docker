## What is an image ?
A image includes everthing a App needs to run (all files, and configuration settings):
- Cut-down OS
- Third-Party Libraries
- Application files
- Environment Variables

## What is an Container ?
A container is like a virtual machine in the sense that provides a isolated environment to run our applications.
Can be stopped and restarted. Is just a OS process, but a special kind of process because it was is own File System.

## Commands :
- From : Specify Base image. To start the container __From__ a `basic operation system base image` 
- Workdir : To set a specific dir, after this command all follwing commands will be executed using that working dir.
- COPY : to copy files or directories 
- Add : to add files or directories
- Run : to execute some OS commands (Linux or Windows)
- Env : to set a environment variable 
- Expose : to define the port where the container should run
- User : to choose each user account wiil run the application
- Cmd : To specify the command that should be executured when we start a container
- Entrypoint : To specify the command that should be executured when we start a container
