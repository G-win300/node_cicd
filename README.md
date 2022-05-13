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

