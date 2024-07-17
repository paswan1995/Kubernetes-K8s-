## k8s contd

* __Kube-proxy__

* kube-proxy is responsible for cluster level networking.
* while CNI is responsible for low level networking on Pod.
* kube-proxy which is present on each node helps in Service level abstractions such as node-port, node to pod, pod to pod, pod to service connections.
* kube-proxy manages ipTables and makes routing possible.

# Deployments

* refer: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

* ![preview](images/81.png)
  
* __strategy__: 
      * recreate
      * rollingUpdates  
* refer: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#strategy

* Demonstrate  deployment with some example 

```
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec: 
  minReadySeconds: 10
  replicas: 4
  selector:
    matchLabels:
      app: nginx
  strategy: 
    type: RollingUpdate
    rollingUpdate: 
      maxSurge: 25%
      maxUnavailable: 25%
  template: 
    metadata: 
      labels:
        app: nginx
        version: "v1.0"
    spec:
      containers: 
        - name: nginx-c
          image: nginx 
          ports: 
            - name: nginx 
              containerPort: 80

---
apiVersion: v1 
kind: Service
metadata:
  name: nginx-svc
spec:
  type: NodePort
  selector: 
    app: nginx 
  ports: 
    - name: nginx
      port: 80
      targetPort: 80
      nodePort: 30002

```
 the manifest

* Apply the manifest
![preview](images/82.png)
![preview](images/83.png)

* Lets review some additional commands
* `kubectl rollout status deployments/nginx-deploy` or `kubectl rollout history deployments/nginx-deploy`
* ![preview](images/84.png)
  
* Now lets make some changes in the manifest Refer Here for changes

```
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec: 
  minReadySeconds: 10
  replicas: 4
  selector:
    matchLabels:
      app: nginx
  strategy: 
    type: RollingUpdate
    rollingUpdate: 
      maxSurge: 25%
      maxUnavailable: 25%
  template: 
    metadata: 
      labels:
        app: nginx
        version: "v1.0"
    spec:
      containers: 
        - name: nginx-c
          image: httpd
          ports: 
            - name: nginx 
              containerPort: 80
          resources: 
            limits: 
              memory: "2Gi"
              cpu: "2"

---
apiVersion: v1 
kind: Service
metadata:
  name: nginx-svc
spec:
  type: NodePort
  selector: 
    app: nginx 
  ports: 
    - name: nginx
      port: 80
      targetPort: 80
      nodePort: 30002

```
![preview](images/85.png)
* Now lets assume you didnt like the release and want to go back to previous version (revision=1)
![preview](images/86.png)
  

* # Trail 2

* Write a  deployment spec for jenkins with rolling updates  
     * surge: 40 %
     * unavailable: 40%
     * replicas = 10

```


```

* ## Probes in Pods

* refer: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/

* # Liveness, Readiness and Startup Probes 

* K8s gives the following probes

* __liveness probe__ : This determines whether the application in container is started correctly. If this check fails,  k8s will try to restart the container according to restartPolicy.

* __Readiness probe__ : This determines whether the container is ready to serve requests. if this check fails, the service will not forward the requests to the pod

* __startup probe__: This is added for slow starting  applications, till startup probe is completed, liveness probes will not be executed.

* __Types of checks__ : 
       * exec
       * grpc
       * httpGet
       * tcpSocket  

* Lets write a Pod spec with basic checks
   
   * liveness check postive and negative: 

```

```

![preview](images)

* Refer Here for the manifest with positive and negative readiness probes
![preview](images)

```


```

![preview](images)

* # Exercises

* Try to write a pod manifest for any  application with web interface 
   
   * spring petclinic
   * nop
   * apache
   * httpd
   * tomcat 

* Ensure your manifests always have 
   
   * resources
   * probes
   * ports

* Now try making a replicaset,  deployment and expose using service.





* ![preview](images)![preview](images)![preview](images)![preview](images)![preview](images)![preview](images)![preview](images)![preview](images)![preview](images)![preview](images)![preview](images)