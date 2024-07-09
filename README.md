# AWS Three Tier Web Architecture Workshop

## Description: 
This workshop is a hands-on walk through of a three-tier web architecture in AWS. We will be manually creating the necessary network, security, app, and database components and configurations in order to run this architecture in an available and scalable manner.

## Audience:
Although this is an introductory level workshop, it is intended for those who have a technical role. The assumption is that you have at least some foundational aws knowledge around VPC, EC2, RDS, S3, ELB and the AWS Console.  

## Pre-requisites:
1. An AWS account. If you don’t have an AWS account, follow the instructions [here](https://aws.amazon.com/console/) and
click on “Create an AWS Account” button in the top right corner to create one.
1. IDE or text editor of your choice.

## Architecture Overview
![Architecture Diagram](https://github.com/aws-samples/aws-three-tier-web-architecture-workshop/blob/main/application-code/web-tier/src/assets/3TierArch.png)

In this architecture, a public-facing Application Load Balancer forwards client traffic to our web tier EC2 instances. The web tier is running Nginx webservers that are configured to serve a React.js website and redirects our API calls to the application tier’s internal facing load balancer. The internal facing load balancer then forwards that traffic to the application tier, which is written in Node.js. The application tier manipulates data in an Aurora MySQL multi-AZ database and returns it to our web tier. Load balancing, health checks and autoscaling groups are created at each layer to maintain the availability of this architecture.

## Workshop Instructions:

See [AWS Three Tier Web Architecture](https://catalog.us-east-1.prod.workshops.aws/workshops/85cd2bb2-7f79-4e96-bdee-8078e469752a/en-US)


![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/c1f51fe7-7ff7-4aea-81bc-595b77dd7a75)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/66a02610-8374-4a8c-907e-90363bf9894b)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/9f7b6c68-c434-40ae-931c-848760367b05)

# Give it a unique name, and then leave all the defaults as in. Make sure to select the region that you intend to run this whole lab in. This bucket is where we will upload our code later.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/6d941022-b710-41d9-980e-b614c835f3a1)

# IAM EC2 Instance Role Creation

#1	.Navigate to the IAM dashboard in the AWS console and create an EC2 role.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/3f850f25-74b9-47a9-889d-c10b38e9e240)

# Select EC2 as the trusted entity.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/207f9663-5005-49c2-9fa8-4b7ba33413c3)

#When adding permissions, include the following AWS managed policies. You can search for them and select them. These policies will allow our instances to download our code from S3 and use Systems Manager Session Manager to securely connect to our instances without SSH keys through the AWS console.

•	AmazonSSMManagedInstanceCore

•	AmazonS3ReadOnlyAccess

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/7f7b2c46-3906-489a-a98d-de17525920c4)

# 1.	Give your role a name, and then click Create Role.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/d40b418b-8e96-4a06-a2e9-f092be7990b9)

# VPC and Subnets VPC Creation

# Navigate to the VPC dashboard in the AWS console and navigate to Your VPCs on the left hand side.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/8afbac19-3ca9-4139-bbd5-4307cc3588a1)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/612fadd4-ca36-457d-b8bb-ec208b32ea86)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/8fca0d2f-4d96-4545-8496-99c9c515fbb4)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/919b926e-eb8b-4472-afd6-49cf7a5fed67)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/bfda0f3f-0693-4312-8069-f940faaa1a83)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/60cff25f-2b75-49e7-9870-532b8a70255d)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/7d00e52b-59a2-493c-ba0b-4b40c0ffe20f)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/ab2fc5aa-0911-4de8-9b6b-1d5fba97ff5c)
![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/0886fff0-cfa5-486d-84c8-3f378b59d32b)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/f7bb13b5-1a80-4cc5-9e83-a8d525e3fc5a)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/74bdef3f-88b1-4361-b730-e3da6c443ecb)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/3d675491-e690-4347-a8d0-1370f6d73ea3)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/a89c33eb-23e2-42d2-b717-926fac2746e0)
![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/d76dfc7d-9186-49ff-beb1-5d6685a19b44)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/08d9bed9-bd89-4259-9df2-b42ec9c0db47)
![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/920674e1-3c78-4ff3-98f4-ba5b0572df40)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/a3b2ed61-6054-4ba3-9f02-5c341c8f693b)
![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/4c9927d9-4bb0-4e35-bce9-b15f4b472951)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/81dd5ca6-4edd-44bd-adc5-d6fd07bb9cee)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/0fe45c19-79b9-4330-9b89-8e61082b1253)
![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/c16998b2-7e4f-4b47-8249-6c9ac73ffb13)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/35c21759-2171-4efa-91bb-1f72f72c971e)

# Edit the Explicit Subnet Associations of the route table by navigating to the route table details again. Select Subnet Associations and click Edit subnet associations.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/fb8559ee-fad1-4380-ace4-8d6a922b5292)

# Select the two web layer public subnets you created eariler and click Save associations.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/4ca45979-bb01-4d69-9eb3-a8d05c0fc8ff)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/5b189234-5a83-4b90-a5c7-65db96ba253b)
![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/8d834a78-1188-48fc-91de-3eb17040fa52)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/b00d2cf6-09f7-4836-ac16-2c70a74c83ee)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/45b6d7e0-cd91-4f10-8abd-f3ffec329f1f)
![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/14069193-2d1d-4da9-a32e-95cfddce13b4)

# Security Groups

# #  Security groups will tighten the rules around which traffic will be allowed to our Elastic Load Balancers and EC2 instances. Navigate to Security Groups on the left side of the VPC dashboard, under Security.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/74973ce0-f923-461e-aaed-56328701e5fc)


# The first security group you’ll create is for the public, internet facing load balancer. After typing a name and description, add an inbound rule to allow HTTP type traffic for your IP.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/ff1741db-32b7-4859-9a7d-f2d07be04d4a)


#The second security group you’ll create is for the public instances in the web tier. After typing a name and description, add an inbound rule that allows HTTP type traffic from your internet facing load balancer security group you created in the previous step. This will allow traffic from your public facing load balancer to hit your instances. Then, add an additional rule that will allow HTTP type traffic for your IP. This will allow you to access your instance when we test.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/8d6cf8fd-037c-4d2a-af67-22b89f203279)

#The third security group will be for our internal load balancer. Create this new security group and add an inbound rule that allows HTTP type traffic from your public instance security group. This will allow traffic from your web tier instances to hit your internal load balancer.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/9ed00b7c-6c9c-4437-b12b-71aaab286b7c)

#The fourth security group we’ll configure is for our private instances. After typing a name and description, add an inbound rule that will allow TCP type traffic on port 4000 from the internal load balancer security group you created in the previous step. This is the port our app tier application is running on and allows our internal load balancer to forward traffic on this port to our private instances. You should also add another route for port 4000 that allows your IP for testing.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/b9f2fafd-8f45-455e-a3e1-ffb952a56e0e)

#The fifth security group we’ll configure protects our private database instances. For this security group, add an inbound rule that will allow traffic from the private instance security group to the MYSQL/Aurora port (3306).

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/988bdda5-42d2-40f8-9f0c-672a19ef4e1d)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/f491e0ce-c17a-4748-b6da-e1d4e14ed0f5)

# Subnet Groups  

#Navigate to the RDS dashboard in the AWS console and click on Subnet groups on the left hand side. Click Create DB subnet groups

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/cdb8b818-6bff-4217-bcb5-4c85c3d17040)

# Give your subnet group a name, description, and choose the VPC we created.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/ce4dc241-5f36-4bd5-b11e-1bae020b8e98)

# When adding subnets, make sure to add the subnets we created in each availability zone specificaly for our database layer. You may have to navigate back to the VPC dashboard and check to make sure you're selecting the correct subnet IDs.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/0a963246-9682-4095-a9fd-16ac71a9b4c2)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/490c1150-f33a-4906-bd53-8fb8bf3d67be)
![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/0108747a-35ef-42cc-9b2b-f1e77ee9f1e8)

# We'll now go through several configuration steps. Start with a Standard create for this MySQL-Compatible Amazon Aurora database. Leave the rest of the defaults in the Engine options as default.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/fc37540c-b870-4af7-a3e0-e38cb6c43c66)

# Under the Templates section choose Dev/Test since this isn't being used for production at the moment. Under Settings set a username and password of your choice and note them down since we'll be using password authentication to access our database.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/2fde4be0-7792-4e45-ab2f-57451055a994)

# Next, under Availability and durability change the option to create an Aurora Replica or reader node in a different availability zone. Under Connectivity, set the VPC, choose the subnet group we created earlier, and select no for public access.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/254e2c9d-c3e3-488c-a9ef-61d27674484f)

# Set the security group we created for the database layer, make sure password authentication is selected as our authentication choice, and create the database.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/e34b859c-96fd-4a39-8501-8c8c88c1188d)

# When your database is provisioned, you should see a reader and writer instance in the database subnets of each availability zone. Note down the writer endpoint for your database for later use.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/268fc983-a381-4c45-b0cd-160ce708701a)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/f9905b29-7908-45ec-bcb5-eebdc9e40c5b)

# App Instance Deployment

# Navigate to the EC2 service dashboard and click on Instances on the left hand side. Then, click Launch Instances.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/1d4d5240-33a8-4247-a6be-20e3a932206f)

# Select the first Amazon Linux 2 AMI

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/7f6fcc67-21c7-4fa1-8d06-0b0faab4b264)

# We'll be using the free tier eligible T.2 micro instance type. Select that and click Next: Configure Instance Details.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/89181b74-955f-4751-9be0-ce7e33bfdf16)

# When configuring the instance details, make sure to select to correct Network, subnet, and IAM role we created. Note that this is the app layer, so use one of the private subnets we created for this layer

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/917f2d7c-55b0-429b-9344-c0e17bc7a242)

# We'll be keeping the defaults for storage so click next twice. When you get to the tag screen input a Name as a key and call the instance AppLayer. It's a good idea to tag your instances so you can easily keep track of what each instance was created for. Click Next: Configure Security Group.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/b96a8d9c-9433-489b-87c6-5d4dadbe0fdb)

# Earlier we created a security group for our private app layer instances, so go ahead and select that in this next section. Then click Review and Launch. Ignore the warning about connecting to port 22- we don't need to do that.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/b32a4249-4282-4019-bfe1-763c5fce926a)

# When you get to the Review Instance Launch page, review the details you configured and click Launch. You'll see a pop up about creating a key pair. Since we are using Systems Manager Session Manager to connect to the instance, proceed without a keypair. Click Launch.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/37fa1304-c220-4026-8cb0-2377f3dfe683)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/6d7dfbda-93b3-4e61-a6c0-1c8a80b4cd2c)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/91f0ea78-1270-487b-8c3d-266b5d70d644)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/3bd726ea-bb64-40a0-ad7f-321703c1a17c)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/d90e8fef-6f31-448e-a3e1-e69acb21ad77)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/985ed962-4b69-464e-a443-502681dc6f6c)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/35a01fb3-9dfd-40b3-b8f2-29036e7f7d12)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/a7fc3fed-3e10-4ccb-945a-cb230aa1c247)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/4cf8f1a8-d702-402b-8f21-5a048a1fe70d)


![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/fa684d85-b730-4b3d-9278-08408820b589)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/c5d974f6-a98a-4081-9031-eb3aebfe54f2)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/dd237759-b9ad-4ed9-9e9a-ba10f90e884d)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/341deb7e-cb63-49ee-9d29-d829993e7bbf)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/b1ad4799-01f9-4df5-83d3-71fa2179f7b2)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/62d0f819-33a3-4360-870b-aa3292706402)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/27e9b6a8-9e98-4e3a-8ff4-9db7595622ab)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/a9a05213-9f73-4c8f-acb5-f0765a6df818)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/662292a4-1f07-4f09-aba7-a6c90e388cb9)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/c14659e7-8233-4a62-b2ee-1265a58f39f2)

#  App Tier AMI

# Navigate to Instances on the left hand side of the EC2 dashboard. Select the app tier instance we created and under Actions select Image and templates. Click Create Image.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/0f1ee566-7a75-49ea-8106-a399dbd902b2)

# Give the image a name and description and then click Create image. This will take a few minutes, but if you want to monitor the status of image creation you can see it by clicking AMIs under Images on the left hand navigation panel of the EC2 dashboard

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/36aca4e2-fabf-4c4b-9c5e-376413e40ef3)

# Target Group

# While the AMI is being created, we can go ahead and create our target group to use with the load balancer. On the EC2 dashboard navigate to Target Groups under Load Balancing on the left hand side. Click on Create Target Group

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/65d23d27-0819-4176-b799-3161adbc8755)


# The purpose of forming this target group is to use with our load blancer so it may balance traffic across our private app tier instances. Select Instances as the target type and give it a name.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/b5d7d850-d535-4377-a10c-cdf700b486a1)


# Then, set the protocol to HTTP and the port to 4000. Remember that this is the port our Node.ja app is running on. Select the VPC we've been using thus far, and then change the health check path to be /health. This is the health check endpoint of our app. Click Next.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/8903ae94-9b2a-460b-9a7a-6d58ae0fbed1)

# We are NOT going to register any targets for now, so just skip that step and create the target group.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/c2c6a888-e5d6-46f8-b862-3a4cc1b2559a)

# Internal Load Balancer -On the left hand side of the EC2 dashboard select Load Balancers under Load Balancing and click Create Load Balancer.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/8000489f-c605-44ed-9f3a-f35079d44d13)

# We'll be using an Application Load Balancer for our HTTP traffic so click the create button for that option.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/ea89e5f7-2d06-4847-b1a7-24a7568c476a)

# After giving the load balancer a name, be sure to select internal since this one will not be public facing, but rather it will route traffic from our web tier to the app tier.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/acb1850d-b695-431f-8ecf-20976901ad59)

# Select the correct network configuration for VPC and private subnet

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/a00fc40d-9462-4601-9cbf-522d4f8ced79)

# Select the security group we created for this internal ALB. Now, this ALB will be listening for HTTP traffic on port 80. It will be forwarding the traffic to our target group that we just created, so select it from the dropdown, and create the load balancer.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/9d00ffa7-d353-40f4-b6f7-8822907209d5)

# Launch Template
# Before we configure Auto Scaling, we need to create a Launch template with the AMI we created earlier. On the left side of the EC2 dashboard navigate to Launch Template under Instances and click Create Launch Template.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/8264f85d-299d-49bc-8b2c-7fa4e7f2eea8)

# Name the Launch Template, and then under Application and OS Images include the app tier AMI you created.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/a9443a75-39ef-4489-9894-e702e2e28451)

# Under Instance Type select t2.micro. For Key pair and Network Settings don't include it in the template. We don't need a key pair to access our instances and we'll be setting the network information in the autoscaling group.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/9cccd819-4303-448d-9e57-8eeca3a7cfc3)

# Set the correct security group for our app tier, and then under Advanced details use the same IAM instance profile we have been using for our EC2 instances.

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/4bed1eee-6a8d-4134-b121-8e53d380b5e0)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/b12b715a-4a19-42e5-8a60-40e269bea7e3)

![image](https://github.com/Siddhartha082/AWS--3-Tier--web-Architecture-/assets/110781138/f13462aa-a3a7-4bd5-bf39-d5bc124fc415)































































































































































































































































