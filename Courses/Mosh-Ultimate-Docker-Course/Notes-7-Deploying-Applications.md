## Examples of problems : 
### Example 1 : Running NGINX with non-root user. 
By having the Docker file of the frontend application with the following Dockerfile : 
```yaml
# Step 1 : Build Stage
FROM node:14.16.0-alpine3.13 AS build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Step 2 : PRD server
FROM nginx:1.12-alpine AS production-stage
RUN addgroup app && adduser -S -G app app
USER app 
COPY --from=build-stage /app/build /usr/share/nginx/html
EXPOSE 80
ENTRYPOINT [ "nginx","-g","daemon off;" ]
```

So, we need to have something like that, to run NGINX as root user.
``` yaml
# Step 1 : Build Stage
FROM node:14.16.0-alpine3.13 AS build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Step 2 : PRD server
USER root
FROM nginx:1.12-alpine AS production-stage
COPY --from=build-stage /app/build /usr/share/nginx/html
EXPOSE 80
ENTRYPOINT [ "nginx","-g","daemon off;" ]
```

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

## What is the different between NPM and a Web Server (in this case we use NGINX) ?
In production we want to have optimzed assets of an application. Also, the Node runtime cames with a small, few features, web server that is __not suited for production__, for production we need a real Web Server :). A _real server_ could be a web server like IIS, Apache or NGINX.

