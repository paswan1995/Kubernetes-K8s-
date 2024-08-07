# Kubernetes Pod(s) 

# Q; i am using my desktop in my desktop i have kubectl  but in my company there are 5 k8s clusters how can use same kubectl for multiple clusters
__ans: go in kubectl context section__

* __Pod Life cycle__ 
    * Pod-Phases : https://kubernetes-docsy-staging.netlify.app/docs/concepts/workloads/pods/pod-lifecycle/
        * A Pod's `status` field is a PodStatus object, which has a `phase` field. 
    
    * Container states in Pod : https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-states

* __Container restart policy__: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/          #restart-policy
       * when a request for a pod creation arrives to api server its stored the details in `etcd` and inform the schedualer to schedule the pod on a node by identifiying suitable node and informs the kubelet. 
       * kubelet with the help of container runtime create a container in the pod. 
       * Each pod get an ip address with the help of cni plugin.
       * CNI plugin is responsible for low level networking to pod.
![preview](images/54.png)  

* __Choosing CNI Plugin__
   * Calico:
       * Network policy: supported
       * Used for large clusters
   * Flannel
       * Network policy: unsupported
       * For dev, test environments,
   * Weavenet
       * Network policy: supported
       * Simple and seamless networking, suitable for small clusters
   * Cilium
       * Network policy: supported
       * using eBPF networking standard which implements the network observability. Generally used for large enterprise applications
   * AWS VPC-CNI:
       * This CNI implemented by AWS to create Pods in Elastic Kubernetes Service which are VPC functionality aware.
   * Azure CNI
       * This CNI implemented by Azure to create Pods in Azure Kubernetes Service which are VNet functionality aware.
    
* __Container types in Pod__
   * Inside pods we can create the following types of containers
       * init container
       * container: these are main contianer which run the application
       * ephemeralContainers
       * sidecarContainers
# Trail 5:

* Creates a k8s pod manifest with the following
   * init container: create a alpine container with sleep 30s 
   * container: run nginx or httpd 

```
---
apiVersion: v1
kind: Pod 
metadata:
  name: trail5
spec:
  restartPolicy: OnFailure
  initContainers:
    - name: init1
      image: alpine
      args:
        - sleep
        - 30s 
  containers:
    - name: nginx
      image: nginx:1.27
      resources:
        requests:
          memory: 128 Mi
          cpu: 250m
        limits:
          memory: 0.5Gi
          cpu: 1000m

```
![preview](images/56.png)
![preview](images/57.png)

* Lets add two more init continers with sleep 10s and add one more container in containers

```
apiVersion: v1
kind: Pod
metadata: 
  name: trail6
spec: 
  restartPolicy: OnFailure
  initContainers: 
    - name: init2
      image: alpine
      args:
        - sleep
        - 10s
    - name: init3
      image: alpine
      args:
        - sleep
        - 10s
  containers:
    - name: nginix
      image: nginx
      resources:
        requests:
          memory: 128Mi
          cpu: 250m 
        limits:
          memory: 0.5Gi
          cpu: 1000m
    - name: sidecar1
      image: alpine
      args:
        - sleep
        - 1d
      resources:
        requests:
          memory: 128Mi
          cpu: 250m
        limits:
          memory: 0.5Gi
          cpu: 1000m

```

![preview](images/58.png)
* __sidecar enhance addons feature like log monitoring__
* if your application doesnt have any pri-condition so dont write init containers, if has then write otherwise no need.

* Exercise:
* try to fail init 2 by cmd exit 1 i.e. error code observe the behavior


* Purpose of init containers: to configure any preconditions for running your applications in container 
     * changing configuration values
     * data correctness check
     * migrate data (orm to db data creation)
 
* controller objects: they ensure pods are running which include
     * Replicasets 
     * Replication Controller
     * Daemonsets
     * Deployments


# Labels

* k8s trys to forward the request to any pods which has these orange lables
![preview](images/59.png)
* k8s groups the objects with the hepl of labels 
* k8s never try to tell that forward this request to the  pod which has these containers inside this 

* k8s stores the data of objects in etcd and it fetches the data of related objects with the help of labels
* Label in k8s is a key value used to group objects logically
* or official docs: https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/
* labels can be selected/queried by two types of queries
     * equality operators: Refer: https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#equality-based-requirement
     * equals (=) and 
     * not equals (!=)
     * set based operators : https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#set-based-requirement
          * in 
          * not in

# trail 6   

* Create a pod manifest with the following labels
     * env = dev 
     * app = nginx
     * version = 1.0
     * for the manifest
```
---
apiVersion: v1
kind: Pod
metadata:
  name: trail6
  labels:
    env: dev
    app: nginx
    version: "1.0"
spec:
  containers:
    - name: nginx
      image: nginx
      resources:
        limits:
          cpu: 500m
          memory: 512Mi

```
![preview](images/60.png)

# Replica Set

* __in metadata section we write a label for replicaset and in template we write a label for pod__
* __selector: the lables which will select your pod__
* __with the help of template you are going to create a pod__
* __You are going to create a pod using a ReplicaSet. The specification of the pod will be described in the template. (replicaset ko use kareke aap pod banane wale ho o pod ka specification kya hai o template me batao ge)__

* for official docs: https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/

![preview](images/55.png)

# Trail 1

* Create 3 nginx pods in a replica set with manifest

```
---
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: trail1-rs
  labels: 
    name: trail
spec: 
  minReadySeconds: 10 
  replicas: 3 
  selector: 
    matchLabels: 
      app: nginx 
  template: 
    metadata:  
      labels: 
        app: nginx 
        env: dev
        version: "1.0"
    spec: 
      containers:
        - name: nginx 
          image: nginx 
          resources: 
            limits: 
              cpu: 500m
              memory: 512Mi
```

![preview](images/61.png)
![preview](images/62.png)


# trail 2

* create 3 pods manually with label app=nginx and then create the rs from trail1
* replicaset will not create a new pod as long as manual pods created above are running as the desired is already met
![preview](images/62.png)

# Exercise

* create a replicaset with pod spec running alpine container without any args

```
---
apiVersion: apps/v1
kind: ReplicaSet
metadata: 
  name: exercise1
  labels:
    app: exercise1
spec:
  minReadySeconds: 5
  replicas: 3
  selector:
    matchExpressions: 
      - key: xyz 
        operator: In 
        values: 
          - exercise1
          - exercise2
  template:
    metadata:
      name: exercise1
      labels: 
        xyz: exercise1
    spec: 
      containers:
        - name: withoutargs
          image: alpine
          resources:
            requests: 
              memory: "64Mi"
              cpu: "250m"
            limits:    
              memory: "128Mi"
              cpu: "500m"

```

# Replication Controller (RC)

* __Replicaset__ is the replacement for __Replication controller (RC)__

* RC can perform only equavality based label selections on Pods where as RS supports set based criteria
* RS supports rolling updates which is used in Deployments, (RS is used by Higher objects such as Deployments and Daemonsets supporting zero downtime deployments)

# Trail3

* Create a manifest for ReplicationController with 3 nginx pods with label `app=nginx`

