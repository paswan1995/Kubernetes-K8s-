## Write a Pod Spec for Spring PetClinic and nopCommerce Applications

```
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: petclinic
spec:
  minReadySeconds: 3
  replicas: 2
  selector:
    matchLabels:
      app: petclinic
  template:
    metadata:
      name: petclinic
      labels:
        app: petclinic
    spec:
      containers:
      - name: petclinic
        image: redfiree/spc
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: petclinic-service
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 8080
  selector:
    app: petclinic
```
