# SampleMERNwithMicroservices

This application has 3 microservices, 2 for the backend and 1 for the frontend.
```
tree --filelimits 3 MERN_Microservices_EKS_Deployment/
```
```
MERN_Microservices_EKS_Deployment/
├── README.md
├── backend
│   ├── README.md
│   ├── helloService  
│   └── profileService  
└── frontend 
```
## Prerequisites
   1: EC2 (min of 4Gb ram and 20 GB disk)

2: Install aws-cli in it 

3: Jenkins installed in it

4: Install docker in it

5: Install EKSCTL in it

6: Install Kubectl in it


![image](https://github.com/AdarshIITDH/SampleMERNwithMicroservices/assets/60352729/73977351-6211-445d-af38-9e6151a49663)

### Prepare the MERN Application

1. Containerize the MERN Application:

   - Ensure the MERN application is containerized using Docker. Create a Dockerfile for each component (frontend and backend).
  
      For Backend Microservice
      https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/blob/main/backend/README.md

      For Frontend Microservice
      https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/tree/main/frontend

2. Push Docker Images to Amazon ECR:

   - Build Docker images for the frontend and backend.

   - Create an Amazon ECR repository for each image.

   - Push the Docker images to their respective ECR repositories.
  
     Hello Microservice: https://gallery.ecr.aws/c3w1m1q2/hello_service_adarsh
     
     Profile Microservice: https://gallery.ecr.aws/c3w1m1q2/profile_service_adarsh
     
     Frontend Microservice: https://gallery.ecr.aws/c3w1m1q2/frontend_service_adarsh


