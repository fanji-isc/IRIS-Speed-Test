# Setting Up and Running the Project on AWS EC2

This guide will help you set up an AWS EC2 instance and run the SpeedTest on it. Follow these steps to deploy the project and start the containers on the EC2 instance.

## Prerequisites
Before proceeding, make sure you have:
- An AWS account.
- An AWS key pair.

## Step 1: Launch an EC2 Instance

1. **Log in to AWS Management Console**:
   - Go to [AWS EC2 Console](https://console.aws.amazon.com/ec2/).
   - Choose **Launch Instance** to create a new EC2 instance.

2. **Name and tags**
   - Name your instance as "SpeedTest"

3. **Application and OS Images (Amazon Machine Image)**
   - Quick Start:
      - Select an AMI (Amazon Machine Image): Amazon Linux 2 AMI Server
      - Select Architecture: 64-bit(x86)

4. **Instance Type**
   - Select t2.2xlarge as an instance type.

5. **Key pair**
   - Choose an existing key pair or create a new one.

6. **Network settings**
   - Firewall:
      - Create security group
      - Check"Allow SSH traffic from" select "Anywhere"
7. **Configure storage**
   - Select 1 x 16 Gib gp3 Root volume
   - Ensure that port 22 (SSH) is open for connecting to the instance.

8. **Launch the Instance**:
   - Click **Launch**.

## Spet 2: Edit Inboud Rules
   - Navigate to your Instance console and click the instance ID you created
   - In Security tab, expand inbound rule,click Security groups,click Security ID
   - In Inbound rules tab,click Edit inbound rules
   - Add rule, select Type "Custom TCP" ,Port range "10000", Source "Custom" , CIDR blocks 0.0.0.0/0
   - Save rules

## Step 3: Connect to Your EC2 Instance

1. **Access the EC2 Instance**
   - Navigate to your Instance console, select the SpeedTest instance you created,click connect 
   - EC2 Instance Connect:
      - Connection Type: select "Connect using EC2 Instance Connect"
   - Click "Connect"

2. **Install Docker and docker-compose on your EC2  instance**
   Run with the following command in your SSH terminal
   ```bash
   sudo yum install -y docker
   sudo service docker start 
   sudo usermod -aG docker ec2-user
   newgrp docker

   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose 
   ```
## Step 4 : Run the Speed Test 
1. **Run it with InterSystems IRIS Community**
   - Run the below command in your SSH terminal

      ```bash
      wget https://raw.githubusercontent.com/fanji-isc/IRIS-Speed-Test/refs/heads/main/docker-compose.yml
      docker-compose up
      ```
   - Once all the containers are up and running, open your web browser and navigate to the following URL:
      http:*//YourPublicIP:10000*

2. **Run it with Postgres**
    - Run the below command in your SSH terminal

      ```bash
      wget https://raw.githubusercontent.com/fanji-isc/IRIS-Speed-Test/refs/heads/main/docker-compose-postgres.yml
      docker-compose -f docker-compose-postgres.yml up
      ```
   - Once all the containers are up and running, open your web browser and navigate to the following URL:
      http:*//YourPublicIP:10000*

3. **Run it with SQLServer**
    - Run the below command in your SSH terminal

      ```bash
      wget https://raw.githubusercontent.com/fanji-isc/IRIS-Speed-Test/refs/heads/main/docker-compose-sqlserver.yml
      docker-compose -f docker-compose-sqlserver.yml up
      ```
   - Once all the containers are up and running, open your web browser and navigate to the following URL:
      http:*//YourPublicIP:10000*

4. **Run it with MySQL**
    - Run the below command in your SSH terminal

      ```bash
      wget https://raw.githubusercontent.com/fanji-isc/IRIS-Speed-Test/refs/heads/main/docker-compose-mysql.yml
      docker-compose -f docker-compose-mysql.yml up
      ```
   - Once all the containers are up and running, open your web browser and navigate to the following URL:
      http:*//YourPublicIP:10000*

