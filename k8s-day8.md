# Managed Kubernetes (Kubernetes as a Service)

* All the CSP offer k8s as a service 

      * AWS = EKS
      * Azure = AKS
      * GCP = GKE

* Architecture of k8s as a service

* All the clouds manage control plane and charge hourly for that
* Nodes can be added by at normal virtual machine costs

![preview](images/90.png)

* K8s as a service provides node autoscaling
* They provide options for 
      * __Networking__
          
           * integrate with cloud load balancers
           * integrate with cloud virtual networks
           * support for layer 7 load balancing with ingress
           * support for third party cni
     
      * __Storage__   
      
           * Volume integration with cloud based disk storages and other storage options
           
     *  __Authentication and authorization (A & A)__ 
           
           * support k8s native A & A
           * extends A & A to cloud based IAM
   
     *  __Administration:__
      
           * Backup of k8s clusters
           * Upgrading k8s clusters
    
     *  __Pod based billing__

# AKS: Azure kubernetes Cluster

* for official docs of Azure kuberentes service. 
* refer: https://learn.microsoft.com/en-us/azure/aks/

*  for quick start to create aks cluster
*  refer: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli

* # Namespaces

* Namespace is a logical cluster for organizing k8s resources.

* By default in k8s cluster we have following namespaces 
      * default
      * kube-system
      * kube-public
* Kuberentes resources can be scoped to a 
      * namespace (namespaced = true)
      * cluster (namespace = false)

* use th namespaced section in `kubectl api-resources` to find out the scope    
      * examples of namespace scope 
          * pods
          * services
          * deployments
          * .....

* examples of cluster scope  
      * node
      * persistent volumes

* Namespaces are generally used to 
      * differentiate environments
      * assign resource limits to the namespaces

* kubectl command can query the default namespace 
* Refer Here: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/

```
kubectl config set-context --current --namespace=dev
```     

*  note: Generally namespace is an administration convinience, adding namespaces in yaml might not be a good practice. 
*   Lets deploy an nginx pods and a service in dev namespace. Refer Here for manifests

```

```
![preview](images)

* Lets create an nginx pod in default namespace
```

```
![preview](images) 

* for namespace and dns
* refer: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#namespaces-and-dns

* Lets try providing Resource Quotas to Namespace 
* Refer Here: https://kubernetes.io/docs/concepts/policy/resource-quotas/

* # LimitRange : 
* refer: https://kubernetes.io/docs/concepts/policy/limit-range/

* # NetworkPolicy 
* refer: https://kubernetes.io/docs/concepts/services-networking/network-policies/
   
