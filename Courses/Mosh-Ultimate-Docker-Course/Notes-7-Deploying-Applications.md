# Questions :
## What is the difference between a Single-Host deployment and a Cluster-deployment ? 
R: Deployment to a machine is much more easy but that server goes offline our application will became unacessible (so `we dont have high availability`), also if the number of users start to grow a lot a single server might not be able to handle the load ( so `we dont have high scalibility`). We can always start with a single-deployment 
and if we see that the number of users starts growing we can upload to a cluster. To have a cluster (group of servers) 
<br><br/>

## What is a `docker-machine` ?
R: Is a tool with each we can setup quickly our servers with docker and with SSH, for later `talk` to them. It can setup this on Cloud-providers, 
our own server.
> Machine lets you create Docker hosts on your computer, on cloud providers, and inside your own data center. It creates servers, installs Docker on them, then configures the Docker client to talk to them.

## Can we use `docker-machine` to connect to setup a local machine ? 
Yes, we can, if i have server on my private network and not in the cloud providers i can set the `Driver` to `None` on the creation step : 
``` powershell
docker-machine create --driver none # (...)
```

## What is SSH (Secure Shell) ? 
Is a protocol to communicate/connect with servers with security. With SSH we can open a secure shell session with out server. Remember a shell is a application
that allows to pass command to the OS. 
