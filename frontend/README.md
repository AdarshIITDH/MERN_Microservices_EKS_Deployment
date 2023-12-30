# Frontend Micro Service

In Frontend microservice it will connect to both the backend microservice helloservice and profile service.

```
cd frontend
```
Inside the frontend microservice create a .env file for dynamically changing the backend urls for both hello microservice and profile microservice

```
nano .env
```
```
REACT_APP_API_URL=$REACT_APP_API_URL
REACT_APP_API_HELLO=$REACT_APP_API_HELLO
```

Now let's containerise the frontend microservice
```
FROM node:18
WORKDIR /
COPY . /
ENV REACT_APP_API_URL $REACT_APP_API_URL
ENV REACT_APP_API_HELLO $REACT_APP_API_HELLO
RUN npm install
CMD ["npm", "run", "start"]
```

Lets build the Docker Image of the Frontend Microservice
```
docker build -t fe_svc .
```
Lets test the Docker container with the environment variables
```
docker run -it -e REACT_APP_API_HELLO=http://<ec2 public ip>:3001 -e REACT_APP_API_URL=http://<ec2 public ip>:3002/fetchUser -p 3000:3000 fe_svc
```
![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/80d211c5-cbb5-44d9-a5bb-200e546ab6b8)


Now push the image to the ECR

```
public.ecr.aws/c3w1m1q2/frontend_service_adarsh
```
https://gallery.ecr.aws/c3w1m1q2/frontend_service_adarsh
![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/e8561d9b-6c53-41d8-bae5-13daad36bc23)


