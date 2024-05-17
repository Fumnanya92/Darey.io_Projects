# Deploying ALB(Application load balancer) with 2 instances 

# Task 1: Create Two EC2 Instances

## Step 1: Log in to the AWS Management Console

- Open your web browser and go to the AWS Management Console at [https://console.aws.amazon.com/](https://console.aws.amazon.com/).
- Enter your AWS account credentials (username and password) and click "Sign In".

## Step 2: Navigate to the EC2 service

- Once logged in, click on "Services" in the top left corner of the console.
- In the search bar, type "EC2" and click on "EC2" from the options that appear.

## Step 3: Use the UserData Script

- Copy the following UserData script:
  
  ```bash
  #!/bin/bash
  yum update -y
  sudo yum install -y httpd httpd-tools mod_ssl
  sudo systemctl enable httpd 
  sudo systemctl start httpd
  ```

  Step 4: Launch two EC2 instances in the same subnet
- Click on "Instances" in the EC2 dashboard.
- Click on the "Launch Instance" button.
- Choose an Amazon Machine Image (AMI), instance type, and configure other instance details as required.
- In the "Configure Instance Details" step:
- Choose the same subnet for both instances to ensure they are in the same network.
- Paste the UserData script into the "Advanced Details" section under "User data".
- Complete the instance launch process by configuring storage, adding tags, configuring security groups, and reviewing the instance launch details.
- Click on "Launch Instances" to launch both EC2 instances.

