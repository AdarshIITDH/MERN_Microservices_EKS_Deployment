## Backend Service

```
tree --filelimit 3 backend/
```
```
backend/
├── README.md
├── helloService  
└── profileService  
```

### Hello Microservice
```
cd helloService
```
Inside the helloservice create a .env file for dynamic hosting the application at available port
```
nano .env
PORT=$PORT
```
Inside the helloservice create a Dockerfile which will help to containerize the hello microservice
```
nano Dockerfile
```
```
FROM node:18
WORKDIR /
COPY . /
RUN npm install
ENV PORT 3001
CMD ["node", "index.js","3001"]
```
Build the docker image
```
docker build -t be_hello_svc:latest .
```
Lets try to test the helloservice container
```
docker run -it -e PORT=3001 -p 3001:3001 be_hello_svc:latest
```
![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/d3ca9c67-298c-4850-8565-98da03952b2c)

![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/c2cc0c49-a022-46a4-bd6b-e21f3d1f74b5)


Now will push the image to ECR
```
public.ecr.aws/c3w1m1q2/hello_service_adarsh:latest
```
https://gallery.ecr.aws/c3w1m1q2/hello_service_adarsh

![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/7badf844-e56a-42a8-af8a-99481eecf998)


### Profile Microservice
```
cd profileService
```
Inside the profileservice create a .env file for dynamic hosting the application at available port and pass the MONGO URL
```
nano .env
PORT=$PORT
MONGO_URL=$MONGO_URL
```
Inside the profileservice create a Dockerfile which will help to containerize the profile microservice
```
nano Dockerfile
```
```
FROM node:18
WORKDIR /
COPY . /
RUN npm install
ENV PORT 3002
ENV MONGO_URL MONGO_URL
CMD ["node", "index.js","3002"]
```
Build the docker image
```
docker build -t be_profilesvc .
```
Lets try to test the profileservice container
```
docker run -it -e MONGO_URL="your mongo url" -p 3002:3002 be_profilesvc:v1
```
![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/900834f9-569f-4cec-8f2c-b6d3d3c793d4)

![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/3af78a36-8640-48b1-92d6-5db4bf658856)


Now will push the image to ECR
```
public.ecr.aws/c3w1m1q2/profile_service_adarsh:latest
```
https://gallery.ecr.aws/c3w1m1q2/profile_service_adarsh

![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/622b3cc4-8ad5-4c9d-89e7-3ce663ee34da)


## Frontend Service
```
cd frontend
```
Inside the frontend microservice create a .env file for dynamically changing the backend urls for both hello microservice and profile microservice







