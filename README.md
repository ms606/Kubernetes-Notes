# Kubernetes-Notes
Notes
## Pods
1. Smallest units of k8s are called Pods. 
2. Pods are abstraction over a containers. 
3. Pods create a layor over the container
4. Usually 1 application per pod. 
5. Each pods get their own IP addresss.
6. As the pods can easily die, like when they lose a db contaner or an app crashed or a node server ran out resource and then new one will be created and it will get the new ip address. 
7. Pod is a layer of abstraction on top of containers. 

## Service
1. So, we have **service**, which is a static ip address that is attached to each pods, app will have its own service (static ip) and the pod will have its own service (static ip).
2. Lifecyle of Pod and service are not connected, so even if the pod dies service and the ip address stay. Our end points remains the same. 

## Ingress
1. Provides a masking type thing which links to service. 
EG, IP Address on the service = https://124.53.342.34:8080 
But this is not practical for the production build so what ingress does is https://my-app.com 
2. The IP address is added in the application code. 
3. In k8s there is a component called **ConifgMap**, this is a external configration of your application, it has URLs, so when you just update the end point i.e. DB_URL = ....., it automatically rebuilds and publish the code. 
4. Do not store the password or anything in ConfigMap, k8s has a component called **Secret**

## Volume (Datastorage)
1. On the restart of the pods all the data will be gone, but we need the data to be constant and persistant, so the way to do is it use the component called Volumes. 
2. The way it works is you add a storage device locally in the K8s cluster, or have a remote storage outside of the cluster like a cloud storage and you add an outside reference on it. 

### What happens when Pods dies or crashes ?
So, lets say our one node server application pod or DB pod dies and crashes, the client will feel the downtime, so to avoid that we will replicate the same node server 1 to node server 2, using ***Service***. Service has two functionalities, 1. it keeps permanent IP and it also performs as a load balancer. 

Service, will catch the request and forward it to whichever pod is least busy. 

#### How to do it ? 
1. We will define a blueprints for pods, this means "create deployments". 
2. In deploymenets you mention how many replicates of pods you want, you want to scale up or down. 
3. Deployment is another abstraction on top of pods. 
4. This deployment is done for the app pod and not the database pod. 
5. For the **database pods** we have a component call **StateFulSet**. 

## K8s Architecture
### Worker machine in k8s cluster
1. Each node has multiple pods (application pod, db pod etc)
2. 3 process must be installed on every nodes
   a. Container runtime
   b. Kubelet (It interacts with both - the container and the node. It also starts the pod with a container inside)  
   c. DB Service, communication between two nodes 
   d. Kube proxy, responsible for sending the communication from DB Service to pods. It must be installed on every node. It has the ability to control the logic flow, eg. If DB service is sending the request to Node 1 - Pod 1 for App , so the Kube Proxy will tell the DB service to check the Node 1 - Pod 1 for DB and not go to any other Node to check for the DB.
3. Nodes are the actual worker nodes that do the work. 

### Master processes
4 processes run on the master node 
  1. API Server: It is an initial cluster gateway, it gets initial request from the Client that can be a UI, update or query.
   Acts as a gatekeeper for authentication. Anything with the request validates requests or other processes..
  2. Scheduler: Checks all the current nodes, whats the status, how busy it is, and then sends the request to **Kublet** to create a new pod there. 
  3. Controll Manager: When a pod dies or crashes, controll manager detects it and charges starts back on ASAP. 
  4. etcd: Key value store/ cluster brain (CLUSTER STATE INFORMATION ONLY) 
     * What resources are available.
     * Did cluster change the state. 
     * Pods died, Kublets restarted the pods
     * Cluster health.
     * Application deployment health.
     * 
