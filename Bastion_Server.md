# Bastion Server

![image](https://blog.cloud66.com/content/images/2016/03/aws-bastion-host-1.png)

- Also known as jump server
- VM that is used to manage other systems
- Primary access point from the Internet and acts as a proxy to other EC2 Instance
- Intent = to provide access to a private network frome external networks such as the public internet 

## What is a proxy?
- gateway between user and the internet


## Step 1: Creating a DB Instance
- Network: VPC created
- Subnet : Private Subnet
- Enable pulic IP

## Step 2: Create new SG and add required inbound rules

## Step 3: Create a new Bastion intance 
- Network: VPC Create d
- Subnet: Public Subnet
- Enable public IP

## Step 4: Use Bastion public IP to SSH into VM
` ssh -i "DevOpsStudents" @ ubuntuIP`

## Step 5: Use DB instance private IP to ssh in 
- Do this whilst already inside Bastion VM

## Step 6: Make sure to scp the key

`scp -i ~/.ssh/DevOpsStudents.pem DevOpsStudents.pem ubuntu@IP:/home/ubuntu/.ssh/`

- (this has to be done in your OS)

## If a bad permission occurs use chmod 400 on the key 

` chmod 400 FILENAME`

