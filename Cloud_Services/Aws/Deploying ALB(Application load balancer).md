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
  sudo amazon-linux-extras enable php7.4
  sudo yum clean metadata
  sudo yum install php php-common php-pear -y
  sudo yum install php-{cgi,curl,mbstring,gd,mysqlnd,gettext,json,xml,fpm,intl,zip,mysqli} -y
  sudo rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
  sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
  sudo yum install mysql-community-server -y
  sudo systemctl enable mysqld
  sudo systemctl start mysqld
  echo "fs-07d0a7f8f87044530.efs.eu-west-2.amazonaws.com:/ /var/www/html nfs4 nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2 0 0" >> /etc/fstab
  mount -a
  chown apache:apache -R /var/www/html
  sudo service httpd restart

