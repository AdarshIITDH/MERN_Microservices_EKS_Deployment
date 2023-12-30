Backend Service

```
tree --filelimit 3 SampleMERNwithMicroservices/backend/
```
```
SampleMERNwithMicroservices/backend/
├── helloService  
└── profileService 
```

```
cd helloService
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
Now will push the image to ECR
```
public.ecr.aws/c3w1m1q2/be_hello_svc:latest
https://gallery.ecr.aws/c3w1m1q2/be_hello_svc
```







cd profileService

nano .env
PORT=$PORT
MONGO_URL=""


nano dockerfile
```
FROM node:18
WORKDIR /
COPY . /
RUN npm install
ENV PORT 3002
ENV MONGO_URL MONGO_URL
CMD ["node", "index.js","3002"]
```
```
docker build -t be_profilesvc:v1 .
```

```
docker run -it -e MONGO_URL="your mongo url" -p 3002:3002 be_profilesvc:v1
```
```
public.ecr.aws/c3w1m1q2/be_profile_svc:latest
https://gallery.ecr.aws/c3w1m1q2/be_profile_svc
```
```
http://<host ip>:3002/fetchUser
```
