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

 Why we need IAM role for EC2 → It is used by your ec2 instance to create EKS cluster and manage s3 bucket by applying this IAM role it gives the authenticity to your ec2 to do changes in aws account.

## Create IAM role with Administrator Access. 

# Step 4 → Attach the created IAM role with your EC2 machine.

# Step 5 → Building Infrastructure Using terraform

## clone the github repo by →
    - mkdir super_mario
    - cd super_mario
    - https://github.com/KadlagV-05/Deployment-of-super-Mario-on-Kubernetes-using-terraform.git
    - cd Deployment-of-super-Mario-on-Kubernetes-using-terraform/
    - cd EKS-TF
    - edit the backend.tf file by → vim backend.tf
  ### (Note →make sure to provide your bucket and region name in this file otherwise it doesn’t work and IAM role is also associated with your ec2 which helps ec2 to use other services such S3 bucket)


# NOW RUN →

## 1. terraform init
    
<img width="990" alt="t" src="https://github.com/user-attachments/assets/b7400f43-cc7e-4945-b786-1a82e4b0630e">

### When we run terraform init, it sets up your working area, downloads necessary plugins, and makes sure everything is in place so that you can start using Terraform to create, update, or manage your infrastructure. It's like getting all the tools and materials ready before you start building something amazing with your computer.

## 2. terraform validate

<img width="661" alt="t1" src="https://github.com/user-attachments/assets/a39efa6b-8579-4cd5-bae1-794f11f85bcd">

### Terraform validate reviews our code to catch any syntax errors or mistake and gives an output success if everything is no error in the file

## 3. terraform plan

<img width="1634" alt="t4" src="https://github.com/user-attachments/assets/f12df00f-4c3d-42b2-aa34-24d39a005b75">

### Terraform plan is used to see what changes will be made to your infrastructure. By using this command we could review and confirm that everything looks good before giving the final approval to build or modify our application infrasructure It is like the blueprint of the construction project before actually creating or changing anything with Terraform

## 4. terraform apply

### This command tells the machine to go ahead and start creating the resourses. when the command is executed it read the terraform code in the file and start building the infra accordingly.

<img width="1413" alt="t3" src="https://github.com/user-attachments/assets/b4a9c38b-3ae0-4f3b-8870-4f3b90aff919">

# It takes 5 to 10 min for complete setup.

## 5. Below command is used to update the configuration of EKS

  - aws eks update-kubeconfig --name EKS_CLOUD --region us-east-1

### command tells the machine that you are using aws eks service in us-east-1 region and you can use your desired location.


# Step 6 → Creation of deployment and service for EKS

 1. change the directory where deployment and service files are stored use the command → cd ..
 2. create the deployment
```
kubectl apply -f deployment.yaml 
```
<img width="1335" alt="d" src="https://github.com/user-attachments/assets/286aede3-0719-4f90-a2fc-315305ece696">

### deployment.yaml file is like a set of instructions that tells a computer system, "Hey, here's how you should run and manage a particular application " . It provides the necessary information for a computer system to deploy and manage a specific software application. It includes details like what the application is, how many copies of it should run, and other settings that help the system understand how to keep the application up and running smoothly.

 3. Now create the service
```
kubectl apply -f service.yaml
```
<img width="1218" alt="s" src="https://github.com/user-attachments/assets/6a9a8320-a95d-44bc-abfd-8947f93fbb52">

### service.yaml file is like a set of rules that helps computers find and talk to each other within a software application. It's like a directory that says, "Hey, this is how you can reach different parts of our application." It specifies how different parts of your application communicate and how other services or users can connect to them.

 4. Run → 
```
kubectl get all
```
<img width="1202" alt="p" src="https://github.com/user-attachments/assets/5b4355a8-d942-4b72-a966-c3d189510d2b">

 5. Now Run the follwing command to get the load balancer ingress
### This command tells all the details of your application
```
kubectl describe service mario-service
```
<img width="1342" alt="l" src="https://github.com/user-attachments/assets/2afd03c4-ca59-42fc-8435-125cd4af17c5">


# Copy the load balancer ingress and paste it on browser and your game is running


<img width="1792" alt="game" src="https://github.com/user-attachments/assets/0bfbc0c5-f4fc-4af5-a6e8-a916dad4393e">

# PLAY AND ENJOY

### Load Balancer Ingress →
It is a mechanism that helps distribute incoming internet traffic among multiple servers or services, ensuring efficient and reliable delivery of requests.

It’s like having a receptionist at a busy office building entrance who guides visitors to different floors or departments, preventing overcrowding at any one location. In the digital world, a Load Balancer Ingress helps maintain a smooth user experience, improves application performance, and ensures that no single server becomes overwhelmed with too much traffic.
    
# Step 7 → Destroy all the Insrastructure    

### Below commands delete your deployment and service. After service and deployment destruction it will destroy the infrastructure.

```
kubectl delete service mario-service

kubectl delete deployment mario-deployment

cd EKS-TF

terraform destroy --auto-approve

Now Go and terminate EC2 instance.
```

# That’s All Thank You.








    
