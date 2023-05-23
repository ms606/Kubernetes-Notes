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
6. 
