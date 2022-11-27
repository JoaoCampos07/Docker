
### How to make a container access the internet ? 

### Is good practice to create volumnes from the directory where we are running `docker-compose` command ? 
For example, i am in `C:\Sources\Projects\Using-docker-compose` if i run docker-compose having the following docker-compose.yaml file: 
``` yaml
  jenkins:
    image: jenkins/jenkins:2.361.4
    ports:
    - "127.0.0.1:8080:8080"
    volumes:
    - ./jenkins_home_on_host:/var/jenkins_home # Here this directory will be created on C:\Sources\Projects\Using-docker-compose\jenkins_home_on_host is correct ??
```
The directory for bind volume will be created here i running the command, on the dir `C:\Sources\Projects\Using-docker-compose`.
