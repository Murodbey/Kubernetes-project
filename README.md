# Kubernetes-project

## Dear Coder,

When I wrote this code, only I and God 
knew what it was.
Now, only God knows!

So if you are done trying to 'optimize'
this routine (and failed),
please increment the following counter
as a warning
to the next guy:

### total_hours_wasted_here = 67

apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-app-coffee
spec:
  replicas: 2
  selector:
    matchLabels:
      app: demo-app-coffee
  template:
    metadata:
      labels:
        app: demo-app-coffee
    spec:
      containers:
        - name: demo-app-coffee
          image: rafayus/demo-app-coffee:latest
          imagePullPolicy: Always
          ports:
            - name: http
              containerPort: 80
            - name: https
              containerPort: 443
      terminationGracePeriodSeconds: 0
