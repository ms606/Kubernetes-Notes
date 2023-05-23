# Kubernetes-Notes
Notes
## Pods
1. Smallest units of k8s are called Pods. 
2. Pods are abstraction over a containers. 
3. Pods create a layor over the container
4. Usually 1 application per pod. 
5. Each pods get their own IP addresss.
6. As the pods can easily die, like when they lose a db contaner or an app crashed or a node server ran out resource and then new one will be created and it will get the new ip address. 
7. So, we have *service*, which is a static ip address that is attached to each pods, app will have its own service (static ip) and the pod will have its own service (static ip).
8. 
9. 
