# Questions :
## What is the difference between a Single-Host deployment and a Cluster-deployment ? 
Deployment to a machine is much more easy but that server goes offline our application will became unacessible (so `we dont have high availability`), also if the number of 
users start to grow a lot a single server might not be able to handle the load ( so `we dont have high scalibility`). We can always start with a single-deployment 
and if we see that the number of users starts growing we can upload to a cluster. To have a cluster (group of servers) 
