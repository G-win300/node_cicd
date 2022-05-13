## **CICD PIPELINE PROJECT TO DEPLOY TO KUBERNETES CLUSTER USING JENKINS**  
### jenkins integration using kubernetes

---
STEP 1: Get your environment ready
since we are using jenkins as our Continous integration agent, we need to install the necessary plugins it will require.

go to MANAGE JENKINS and install docker pipeline plugin
since we will also be deploying to kubernetes later on, we also need to install kubernetes plugin.
note: the latest kubernetes plugin you'll see is faulty, so we will need to install an earlier stable version. you can download it via this link

STEP: pull our simple application that we need to run from this repo  
create a file called **Dockerfile** and paste this code  
```
FROM node:latest
ENV NODE_ENV=production

WORKDIR /app

COPY ["package.json", "package-lock.json*", "./"]

RUN npm install --production

COPY . .

EXPOSE 3000

CMD [ "node", "index.js" ]
```


---
STEP: still in our current directory, created a deployment-service.yaml file.  
this file contains both our kubernetes deployment and service configuration.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nodeapp-deployment
  labels:
    app: nodeapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nodeapp
  template:
    metadata:
      labels:
        app: nodeapp
    spec:
      containers:
      - name: nodeapp
        image: gwin300/node-app
        ports:
        - containerPort: 3000

---
apiVersion: v1
kind: Service
metadata:
  name: nodeapp-service
spec:
  selector:
    app: nodeapp
  type: NodePort
  ports:
    - protocol: TCP
      port: 8887
      targetPort: 3000
      nodePort: 32000
```

**note:** it should be noted that in this file, we used **nodePort** instead of loadBalancer because we are not using the cloud. 

