# MERN Microservices deployment using EKS

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

### Set Up the AWS Environment

1. Set Up AWS CLI on the EC2:
   - Install AWS CLI and configure it with AWS credentials.
     On your Ec2, run the aws configure --profile command to create an AWS CLI profile to use with git-remote-codecommit. When prompted, provide your AWS access key, your secret access key, the AWS Region where you created your AWS CodeCommit repository, and the default output format you prefer. For example:
      ```
       % aws configure --profile demo-profile
      AWS Access Key ID [None]: ***************
      AWS Secret Access Key [None]: ***************
      Default region name [None]: ap-south-1
      Default output format [None]: 
      ```




  


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

### Version Control

1. Use AWS CodeCommit:

   - Create a CodeCommit repository.
     ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/673cc017-643d-4b66-8c50-3e82150f1ed9)

      Now install the git-remote-codecommit in the EC2
     ```
     apt install python3-pip
     pip install git-remote-codecommit
     ```
     
   - Push the MERN application source code to the CodeCommit repository.

     Now clone the codecommit repo to the ec2
     ```
      git clone codecommit::ap-south-1://adarsh_Microservice_Repo
     ```
     ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/2df8c225-edd0-4f4f-b990-a05171015ed0)
      ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/5521d5c7-cf60-4ba9-8d27-65c1d64449ec)
     ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/1469e48c-20c3-4c6b-a719-0320794664c5)
     ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/31e787b7-1d75-4bba-a92c-9bcd13f44399)
      ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/0d8dc694-57be-4325-a043-861679f9c80e)
  
     Code is sucessfully pushed to code commit
     ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/9a7dca54-c4b5-43e7-a2c3-9d7f2d15c846)




     






