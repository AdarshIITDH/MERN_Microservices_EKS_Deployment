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

### Continuous Integration with Jenkins

1. Create Jenkins Jobs:

   - Create Jenkins jobs for building and pushing Docker images to ECR.

   - Trigger the Jenkins jobs whenever there's a new commit in the CodeCommit repository.





### Kubernetes (EKS) Deployment

1. Create EKS Cluster:

   - Use eksctl or other tools to create an Amazon EKS cluster.

    Installing EKSCTL on EC2 using https://eksctl.io/installation/
    ```
    # for ARM systems, set ARCH to: `arm64`, `armv6` or `armv7`
   ARCH=amd64
   PLATFORM=$(uname -s)_$ARCH
   
   curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
   
   # (Optional) Verify checksum
   curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check
   
   tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz
   sudo mv /tmp/eksctl /usr/local/bin
    ```
    ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/e8f3ee00-e06e-4f4a-93f3-6ecaeb331f10)

    ```
    eksctl create cluster --name mern_microservice_adarsh --region ap-south-1 --nodegroup-name standard-workers --node-type t2.micro --nodes 2 --nodes-min 1 --nodes-max 3
    ```
   ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/57701e75-08b1-4ead-8b82-054252743342)

  
   ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/48e5cfe7-21a5-4156-a545-984b95736a4f)

   ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/74392e18-a507-404c-b8b0-bedad0095f0e)

   ```
   aws eks --region ap-south-1 update-kubeconfig --name mern-microservice-adarsh
   ```
   ![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/83cdb391-b03d-45d1-a09a-d445f5d9abf6)


   Now install kubectl to interact with the cluster    [https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html]

   ```
   curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.28.3/2023-11-14/bin/linux/amd64/kubectl
   curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.28.3/2023-11-14/bin/linux/amd64/kubectl.sha256
   sha256sum -c kubectl.sha256
   chmod +x ./kubectl
   mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH
   echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
   kubectl version --client
   ```
   ```
   aws eks --region ap-south-1 update-kubeconfig --name mern-microservice-adarsh
   ```
   Note if you below error then update awscli version

   error-1: Unable to connect to the server: getting credentials: decoding stdout: no kind "ExecCredential" is registered for version "client.authentication.k8s.io/v1alpha1" in scheme

   error-2: error: exec plugin: invalid apiVersion “client.authentication.k8s.io/v1alpha1

   solution : Update the awscli version
   ```
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   sudo apt install unzip
   unzip awscliv2.zip
   sudo ./aws/install --update
   ```


2. Deploy Application with Helm:

   - Use Helm to package and deploy the MERN application on EKS.
     https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/tree/main/deploy
     



















### Monitoring and Logging

1. Set Up Monitoring:

   - Use CloudWatch for monitoring and setting up alarms.

![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/3e12b93f-6473-4939-ba52-41521fae8703)


![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/ed1b2bab-cc3e-491c-815a-b861d0e5d8ea)


![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/0c8bc73a-d034-4083-9bae-12ebdd0410a9)

![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/d995a3cf-1e5c-4bf3-9b9a-1f93f2c1cef7)


![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/f7a5f8a4-070b-4ea5-9469-45ab855386d5)

![image](https://github.com/AdarshIITDH/MERN_Microservices_EKS_Deployment/assets/60352729/0362a08f-2edc-4c4e-9759-055e7645aee8)




2. Configure Logging:

   - Use CloudWatch Logs or another logging solution for collecting logs.

