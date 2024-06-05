Kubernetes-Activities
DAY-1[26/04/2023]
1.Have the installation of Kubernetes (K8S) cluster by using kubeadm?
2.Write a Pod Spec for Spring PetClinic and nopCommerce Applications?
3.Execute the kubectl commands: kubectl get pods and describe po?
DAY-2[27/04/2023]
1.Explain Kubernetes architecture?
2.Setup k8s on single node using minikube and kind?
3.Run the Spring Pet Clinic application by k8s manisfest file?
DAY-3[28/04/2023]
1. K8s Cluster Installation
   a) kubeadm
   b) minikube
   c) kind
2.Writing the Manifest Files for Spring PetClinic and nopCommerce App
3.Writing the Manifest Files for Game of Life App?
4.Creating Jobs & CronJobs
5.Creating the ReplicaSet and Replication controller?
6.Writing the LABELS and Selecting the LABELS using selector concept?
DAY-4[04/05/2023]
1.Please ensure that, all the Classroom K8S Concepts covered so far, have to be practiced
well both Technically and Theoretically as well for Interviews perspective like:
* Pods / Containers
* Jobs / CronJobs
* ReplicaSets
* Deployment
* Service / Headless Service
* Volumes / Persistent Volumes / Persistent Volume Claims
* Stateful Sets and
* Namespaces etc.
DAY-5[05/05/2023]
1. Create a MySQL pod with Stateful Set with 1 replica
2. Create a nopCommerce deployment with 1 replica
3. Create a Headless Service to interact with nopCommerce with MySQL
4. Create a Load Balancer to expose the nopCommerce to External World
5. NOTE: Try to draw the Architecture Diagram for the above by using Draw.io Tool.
DAY-6[09/05/2023]
1.Create a Kubernetes cluster using kubeadm?
2.Deploy any application using kubectl?
3.Backup Kubernetes I.e backup etcd?
4.List out all the pod’s running in kube system namespace?
5.Write down all the steps required to make Kubernetes highly available?
6.Do a rolling update and roll back?
7.Ensure usage of secret in MySQL and configmaps?
8.Create a nop commerce deployment with MySQL statefulset and nop deployment?
DAY-7[10/05/2023]
1.   Create 1 master node and 2 worker nodes – run app on node1 and db on node2 by using
a. Node selector
b. Affinity
c. Taints and tolerances
     2. Create k8s cluster with version 1.25 and run any deployment(nginx/any) and then upgrade
cluster to version 1.27
DAY-8[16/05/2023]
1. Installing EKS and Aks
2.Installations using helm chart
       1. Mysql
       2. PostgreSql
       3. mongoDB
       3. Redis cache
3.Make Mysql as Stateful set And write headless service for Mysql1
4.write kostomize file by creating files for 3 environments and every environment should
have their own secret?
       1.dev-environment
       2.qa-environment
       3.test-environment