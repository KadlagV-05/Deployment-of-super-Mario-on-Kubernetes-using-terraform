# Project Description: Deployment of Super Mario on Kubernetes using Terraform.

## Overview :
<img width="588" alt="image_2024_07_18T05_10_06_993Z" src="https://github.com/user-attachments/assets/884e4f9d-5465-401b-8e00-20cec810f7ef">



# Step By Step Implementation →

Step 1 → Login and basics setup

Step 2 → Setup Docker ,Terraform ,aws cli , and Kubectl

Step 3 → IAM Role for EC2

Step 4 →Attach IAM role with your EC2

Step 5 → Building Infrastructure Using terraform

Step 6 → Creation of deployment and service for EKS

Step 7 → Destroy all the Insrastructure

Let’s do it


# Step 1 → Login and basics setup

### Launch an EC2 instance with the following setting.
## Allow https,http and set a key pair

<img width="1792" alt="1" src="https://github.com/user-attachments/assets/148f56a0-93da-40a5-8d27-449bf6d2590a">
<img width="1792" alt="2" src="https://github.com/user-attachments/assets/8357eb41-96eb-490f-8b4b-2122697e94c9">
<img width="1792" alt="3" src="https://github.com/user-attachments/assets/6dcc34ad-4941-4a5b-8635-0ea409f24478">
<img width="1792" alt="4" src="https://github.com/user-attachments/assets/ba8636da-8b85-4598-a75d-141a796d5d44">

## Click on connect and you are connected with your machine.

<img width="1792" alt="5" src="https://github.com/user-attachments/assets/7f232c04-aa35-4fa1-be66-636a207c8f92">
<img width="1792" alt="6" src="https://github.com/user-attachments/assets/8d906487-6079-46d7-b732-c50f9b037ba4">

# Step 2 → Setup Docker ,Terraform ,aws cli , and Kubectl.

## Run the following commands after connecting the EC2 machine.
  - sudo su
  - apt update -y
### Setup Docker
  - apt install docker.io
  - usermod -aG docker $USER # Replace with your username e.g ‘ubuntu’
  - newgrp docker
### Setup Terraform
  - sudo apt install wget -y
  - wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
  - echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
  - sudo apt update && sudo apt install terraform
### Setup AWS cli
  - curl “https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o “awscliv2.zip”
  - sudo apt-get install unzip -y
  - unzip awscliv2.zip
  - sudo ./aws/install
### Setup kubectl
  - sudo apt install curl -y
  - curl -LO https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
  - sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

# Every thing is setup and installed now.

# Step 3 → IAM Role for EC2

### Why we need IAM role for EC2 → It is used by your ec2 instance to create EKS cluster and manage s3 bucket by applying this IAM role it gives the authenticity to your ec2 to do changes in aws account.

## Create IAM role with Administrator Access. 

# Step 4 → Attach the created IAM role with your EC2 machine.

# Step 5 → Building Infrastructure Using terraform

  clone the github repo by →
    - mkdir super_mario
    - cd super_mario
    - https://github.com/KadlagV-05/Deployment-of-super-Mario-on-Kubernetes-using-terraform.git
    - cd Deployment-of-super-Mario-on-Kubernetes-using-terraform/
    - cd EKS-TF
    - edit the backend.tf file by → vim backend.tf  
  ### (Note →make sure to provide your bucket and region name in this file otherwise it doesn’t work and IAM role is also associated with your ec2 which helps ec2 to use other services such S3 bucket)


# NOW RUN →

    
    












    
