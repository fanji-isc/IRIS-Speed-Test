# Setting Up and Running the Project on AWS EC2

This guide will help you set up an AWS EC2 instance and run the project on it. Follow these steps to deploy the project and start the containers on the EC2 instance.

## Prerequisites
Before proceeding, make sure you have:
- An AWS account.
- Docker and Docker Compose installed on your EC2 instance.
- A GitHub repository with the project code or Docker image you want to run.

## Step 1: Launch an EC2 Instance

1. **Log in to AWS Management Console**:
   - Go to [AWS EC2 Console](https://console.aws.amazon.com/ec2/).
   - Choose **Launch Instance** to create a new EC2 instance.

2. **Select an AMI (Amazon Machine Image)**:
   - Choose Amazon Linux 2 AMI Server

3. **Choose an Instance Type**:
   - Select t3.2xlarge as an instance type.

4. **Configure Instance**:
   - Set any additional configurations as needed (VPC, security groups, etc.).
   - Ensure that port 22 (SSH) is open for connecting to the instance.
   - Add a security group that allows inbound access on the necessary ports (e.g., 8080, 10000 for your app, or others based on your Docker configuration).

5. **Create or Select a Key Pair**:
   - Choose an existing key pair or create a new one.

6. **Launch the Instance**:
   - After selecting the key pair, click **Launch**.

## Step 2: Connect to Your EC2 Instance

1. **Access the EC2 Instance**:
   - Use SSH to connect to your EC2 instance. Open a terminal and run the following command:

   ```bash

       scp -i /path/to/your-key.pem -r /path/to/your/local/repo ec2-user@<EC2_PUBLIC_IP>:/home/ec2-user/<destination-directory>
   
