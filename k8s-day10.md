# Pod Scheduling

* Pod affinity and antiaffinity

* In this example we had tried to place a pod B

* We want to run the affinity pod on the same node as pod B same node = topology. 
* Topology for node is host name and we want to run antiaffinity pod on the different node

* apply the manifests

```


```

# node affinity

* refer: https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes-using-node-affinity/

* __differences between nodeselector and node affinity__ 
* refer: https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity

# Taint and toleration

* refer: https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/ 

* Lets apply a taint for node1
`kubectl taint nodes aks-nodepool1-19501529-vmss000000 team=devops:NoSchedule`

* Lets create two pods one with toleration and other without toleration

```


```

* Note: We can try Priority class to assign pods a priority


* # Persistent Volumes in Kubernetes (csi= container storage interface)

* Kuberenetes implements Storage as CSI. There are lots of vendors who provide CSI implementations 
* Refer Here: https://kubernetes-csi.github.io/docs/drivers.html

* The interaction with storage is done by CSI

* k8s interacts with CSI to deal with storage

* This option enables dynamic provisioning also

* * k8s is not creating storage its asking to csi to create storage . 

* In managed k8s we have storage classes

![preview](images)

* We can initiate a request from pod for a PersistentVolume (PV) which is referred as Persistent Volume Claim (PVC)

* Lets create a mysql pod with a Persistent volume

* Lets create pvc and apply

```


```

![preview](images)

* Lets apply the pod with pvc

![preview](images)

![preview](images)

![preview](images)

![preview](images)

![preview](images)

* Connect to database and insert some records

* Now lets delete the pod and recreate the pod by applying the manifest

* To statically provision volume 
* Refer Here: https://learn.microsoft.com/en-us/azure/aks/azure-csi-disk-storage-provision#static-provisioning-parameters

* 



priority class 
removing low class 

* create a mysql pod and expose port 3306 with environmental variables 
* 
* when you basically create csi there is something cames into play that is storage class . 
* storage class is  what are types of disk you want to create. 
* k8s has a extra implimentation or has flexibity  to dell with any types you of disk you want to create because of csi and any vendor, or there are many vendors who are selling storage will try to deal or will try to gives you csi driver all you need to do that install in k8s cluster, once you install it in your k8s cluster it will understand external storages also .
* seince it has given plugin option now we can use many external devices in k8s for this we need to write csi implimentation to that way of installing them.

# SMB : 

```
SMB (Server Message Block) in Kubernetes is a way to use network file shares with your Kubernetes pods. Here's a simple explanation:

What is SMB in Kubernetes?
SMB (Server Message Block): It's a network file sharing protocol that allows applications and users to access files on remote servers as if they were on their local computer.
Kubernetes: It's a system for managing containerized applications across multiple hosts.
Using SMB in Kubernetes:
Persistent Volume (PV): This is a piece of storage in the Kubernetes cluster. It can use SMB to connect to a remote file share.
Persistent Volume Claim (PVC): This is a request for storage by a Kubernetes pod. It claims a piece of the Persistent Volume.
Secrets: These are used to store sensitive data like SMB credentials (username and password) securely.
Steps to Use SMB in Kubernetes:
Create a Secret: Store your SMB credentials in a Kubernetes secret.
Define a Persistent Volume (PV): Specify the details of the SMB share in a PV YAML file.
Create a Persistent Volume Claim (PVC): Define how much storage you need and create a PVC YAML file.
Mount the PVC in a Pod: Use the PVC in your pod definition so the pod can access the SMB share.
Why Use SMB in Kubernetes?
Network Storage: It allows Kubernetes pods to access files on a network share.
Shared Storage: Multiple pods can read and write to the same storage.
Flexibility: You can use existing SMB shares without changing your infrastructure.
In essence, SMB in Kubernetes lets your containerized applications use network file shares seamlessly.

```


what are the type of storage which you want to deal with 
persistance volume it is a actuall volume 
persistance volume claim is request that is making like i want to 5gb or i need a 5gb disk that request that pod is making something is called as pvc.
volume is all about disk not about database.

# if you k8s cluster wants to speak with rds so it is a networking issuse not storage issues beacues you need to figure out how your pod is communicate with existing database.


