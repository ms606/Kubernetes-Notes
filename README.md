# Kubernetes-Notes
Notes
## Pods
1. Smallest units of k8s are called Pods. 
2. Pods are abstraction over a containers. 
3. Pods create a layor over the container
4. Usually 1 application per pod. 
5. Each pods get their own IP addresss.
6. As the pods can easily die, like when they lose a db contaner or an app crashed or a node server ran out resource and then new one will be created and it will get the new ip address. 

## Service
1. So, we have **service**, which is a static ip address that is attached to each pods, app will have its own service (static ip) and the pod will have its own service (static ip).
2. Lifecyle of Pod and service are not connected, so even if the pod dies service and the ip address stay. Our end points remains the same. 

## Ingress
1. Provides a masking type thing which links to service. 
EG, IP Address on the service = https://124.53.342.34:8080 
But this is not practical for the production build so what ingress does is https://my-app.com 


