# AWS Autoscaling Group Project

This project demonstrates how to set up an AWS Auto Scaling Group that automatically scales EC2 instances based on traffic demand. The setup includes creating a web server that scales up and down to meet website traffic demands, ensuring efficient use of resources and cost savings.

## Table of Contents

- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
  - [Step 1: Create Public and Private Subnets](#step-1-create-public-and-private-subnets)
  - [Step 2: Write an EC2 UserData Script](#step-2-write-an-ec2-userdata-script)
  - [Step 3: Create an Auto Scaling Group](#step-3-create-an-auto-scaling-group)
  - [Step 4: Create an Application Load Balancer](#step-4-create-an-application-load-balancer)
  - [Step 5: Create Auto Scaling Policies](#step-5-create-auto-scaling-policies)
- [Testing](#testing)
- [Conclusion](#conclusion)

## Architecture

The architecture consists of the following components:

- **VPC** with 3 public subnets and 3 private subnets.
- **EC2 Instances** configured using a UserData script to run a web server (Apache or Nginx).
- **Auto Scaling Group** to manage the EC2 instances.
- **Application Load Balancer** to distribute incoming traffic.
- **CloudWatch Alarms** or **Target Tracking Policies** to trigger scaling activities.

## Prerequisites

- AWS Account
- AWS CLI configured
- Basic understanding of AWS services (EC2, VPC, Auto Scaling, CloudWatch)

## Setup

### Step 1: Create Public and Private Subnets

1. Log in to the AWS Management Console.
2. Navigate to the VPC Dashboard.
3. Create a new VPC if you don't have one.
4. Create 3 public subnets in different availability zones (AZs).
5. Create 3 private subnets in the same AZs as the public subnets.

### Step 2: Write an EC2 UserData Script

Create a UserData script (`userdata.sh`) to install and configure Apache or Nginx on EC2 instances

### Step 3: Create an Auto Scaling Group
1. Go to the EC2 Dashboard.
2. Create a new Launch Configuration:
- Choose an Amazon Machine Image (AMI).
- Select an instance type.
- Configure the details, and add the userdata.sh script under the Advanced Details section as UserData.
- Add storage and configure security groups to allow HTTP (port 80) traffic.
- Review and create the Launch Configuration.
3. Create a new Auto Scaling Group:
- Select the Launch Configuration created earlier.
- Choose the VPC and the subnets created in Step 1.
- Configure scaling policies (we will set up detailed policies in Step 5).

### Step 4: Create an Application Load BAlancer
1. Go to the EC2 Dashboard.
2. Navigate to Load Balancers
3. Create a new Application Load Balancer:
Configure the load balancer to be internet-facing.
Select the VPC and the public subnets.
Configure security settings, security groups, and listeners (HTTP on port 80).
Register targets (Auto Scaling Group).
