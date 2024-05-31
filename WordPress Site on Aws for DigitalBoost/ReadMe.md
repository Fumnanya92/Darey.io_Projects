# WordPress Site on AWS

# 1. Create a VPC

# Guide to Create a Virtual Private Cloud (VPC) for WordPress Infrastructure

## Step 1: Define Address Range for the VPC

1. Determine the CIDR block for the VPC.
   - Example: `10.0.0.0/16`

## Step 2: Create VPC with Public and Private Subnets

1. **Create the VPC:**
   - Navigate to the VPC Dashboard in your AWS Management Console.
   - Click on "Create VPC".
   - Enter the VPC name (e.g., `WordPress-VPC`).
   - Set the IPv4 CIDR block to `10.0.0.0/16`.
   - Select "Default" for Tenancy.
   - Click on "Create VPC".

2. **Create Subnets:**
   - Go to the Subnets section in the VPC Dashboard.
   - Click on "Create Subnet".

   **Public Subnet:**
   - Name: `Public-Subnet`
   - VPC: `WordPress-VPC`
   - Availability Zone: Choose one (e.g., `us-west-2a`)
   - IPv4 CIDR block: `10.0.1.0/24`
   - Click on "Create subnet".

   **Private Subnet:**
   - Name: `Private-Subnet`
   - VPC: `WordPress-VPC`
   - Availability Zone: Choose one (e.g., `us-west-2a`)
   - IPv4 CIDR block: `10.0.2.0/24`
   - Click on "Create subnet".

## Step 3: Configure Route Tables for Each Subnet

1. **Create Route Table for Public Subnet:**
   - Go to the Route Tables section in the VPC Dashboard.
   - Click on "Create Route Table".
   - Name: `Public-Route-Table`
   - VPC: `WordPress-VPC`
   - Click on "Create route table".

   **Add Internet Gateway:**
   - Go to the Internet Gateways section.
   - Click on "Create Internet Gateway".
   - Name: `WordPress-IGW`
   - Click on "Create internet gateway".
   - Select the newly created Internet Gateway and click "Attach to VPC".
   - Choose `WordPress-VPC` and click "Attach".

   **Update Route Table:**
   - Go back to the Route Tables section.
   - Select `Public-Route-Table`.
   - Go to the Routes tab and click on "Edit routes".
   - Click on "Add route".
   - Destination: `0.0.0.0/0`
   - Target: Select `Internet Gateway` and choose `WordPress-IGW`.
   - Click "Save routes".

   **Associate Public Subnet:**
   - Go to the Subnet Associations tab.
   - Click on "Edit subnet associations".
   - Select `Public-Subnet`.
   - Click "Save associations".

2. **Create Route Table for Private Subnet:**
   - Go to the Route Tables section in the VPC Dashboard.
   - Click on "Create Route Table".
   - Name: `Private-Route-Table`
   - VPC: `WordPress-VPC`
   - Click on "Create route table".

   **Update Route Table:**
   - This route table will not have a route to the Internet Gateway, so it uses the default local route.

   **Associate Private Subnet:**
   - Go to the Subnet Associations tab.
   - Click on "Edit subnet associations".
   - Select `Private-Subnet`.
   - Click "Save associations".

## Summary
- **VPC**: `WordPress-VPC` (`10.0.0.0/16`)
- **Subnets**:
  - Public Subnet: `10.0.1.0/24`
  - Private Subnet: `10.0.2.0/24`
- **Route Tables**:
  - Public Route Table with route to Internet Gateway
  - Private Route Table with local route only
- **Internet Gateway**: `WordPress-IGW` attached to the VPC

# Step-by-Step Guide to Implement a Secure Network Architecture with Public and Private Subnets

## Step 1: Set Up Public Subnet for Resources Accessible from the Internet

1. **Create the Public Subnet:**
   - Navigate to the VPC Dashboard in your AWS Management Console.
   - Go to the Subnets section.
   - Click on "Create Subnet".
   - Name: `Public-Subnet`
   - VPC: `Your-VPC`
   - Availability Zone: Choose one (e.g., `us-west-2a`)
   - IPv4 CIDR block: `10.0.1.0/24`
   - Click on "Create subnet".

2. **Create and Attach an Internet Gateway:**
   - Go to the Internet Gateways section.
   - Click on "Create Internet Gateway".
   - Name: `My-Internet-Gateway`
   - Click on "Create internet gateway".
   - Select the newly created Internet Gateway and click "Actions" > "Attach to VPC".
   - Choose `Your-VPC` and click "Attach".

3. **Create and Configure a Route Table for the Public Subnet:**
   - Go to the Route Tables section.
   - Click on "Create Route Table".
   - Name: `Public-Route-Table`
   - VPC: `Your-VPC`
   - Click on "Create route table".
   - Select `Public-Route-Table`.
   - Go to the Routes tab and click on "Edit routes".
   - Click on "Add route".
   - Destination: `0.0.0.0/0`
   - Target: Select `Internet Gateway` and choose `My-Internet-Gateway`.
   - Click "Save routes".
   - Go to the Subnet Associations tab.
   - Click on "Edit subnet associations".
   - Select `Public-Subnet`.
   - Click "Save associations".

## Step 2: Create Private Subnet for Resources with No Direct Internet Access

1. **Create the Private Subnet:**
   - Go to the Subnets section.
   - Click on "Create Subnet".
   - Name: `Private-Subnet`
   - VPC: `Your-VPC`
   - Availability Zone: Choose one (e.g., `us-west-2a`)
   - IPv4 CIDR block: `10.0.2.0/24`
   - Click on "Create subnet".

2. **Create and Configure a Route Table for the Private Subnet:**
   - Go to the Route Tables section.
   - Click on "Create Route Table".
   - Name: `Private-Route-Table`
   - VPC: `Your-VPC`
   - Click on "Create route table".
   - Select `Private-Route-Table`.
   - Go to the Routes tab and click on "Edit routes".
   - Add the default local route automatically provided (`10.0.0.0/16` -> `local`).
   - Go to the Subnet Associations tab.
   - Click on "Edit subnet associations".
   - Select `Private-Subnet`.
   - Click "Save associations".

## Step 3: Configure a NAT Gateway for Private Subnet Internet Access

1. **Create an Elastic IP for the NAT Gateway:**
   - Navigate to the Elastic IPs section in the VPC Dashboard.
   - Click on "Allocate Elastic IP address".
   - Click "Allocate".
   - Note the allocated Elastic IP.

2. **Create the NAT Gateway:**
   - Go to the NAT Gateways section.
   - Click on "Create NAT Gateway".
   - Subnet: Select `Public-Subnet`.
   - Elastic IP Allocation ID: Select the Elastic IP you just created.
   - Click on "Create NAT Gateway".

3. **Update the Route Table for the Private Subnet:**
   - Go to the Route Tables section.
   - Select `Private-Route-Table`.
   - Go to the Routes tab and click on "Edit routes".
   - Click on "Add route".
   - Destination: `0.0.0.0/0`
   - Target: Select `NAT Gateway` and choose the newly created NAT Gateway.
   - Click "Save routes".

## Summary
- **VPC**: `Your-VPC`
- **Subnets**:
  - Public Subnet: `10.0.1.0/24`
  - Private Subnet: `10.0.2.0/24`
- **Route Tables**:
  - Public Route Table with route to Internet Gateway
  - Private Route Table with route to NAT Gateway
- **Internet Gateway**: `My-Internet-Gateway` attached to the VPC
- **NAT Gateway**: Created in the Public Subnet with an associated Elastic IP

  # Step-by-Step Guide to Deploy a Managed MySQL Database Using Amazon RDS for WordPress Data Storage

## Step 1: Create an Amazon RDS Instance with MySQL Engine

1. **Navigate to RDS Dashboard:**
   - Log in to your AWS Management Console.
   - Go to the RDS Dashboard.

2. **Create a New Database:**
   - Click on "Create database".
   - Select the "Standard Create" option.
   - Engine options: Choose `MySQL`.
   - Version: Select the desired MySQL version (e.g., `MySQL 8.0`).

3. **Specify DB Details:**
   - DB instance identifier: `wordpress-db`.
   - Master username: Choose a username (e.g., `admin`).
   - Master password: Set a secure password and confirm it.

4. **Configure Instance:**
   - DB instance class: Choose an instance type (e.g., `db.t3.micro` for testing or `db.t3.medium` for production).
   - Storage type: Select `General Purpose (SSD)` and specify the allocated storage (e.g., `20 GB`).

5. **Set Up Networking:**
   - VPC: Choose the VPC where your WordPress application is running.
   - Subnet group: Select a subnet group that includes subnets in different Availability Zones.
   - Public access: Set to `No` for enhanced security.
   - VPC security groups: Choose or create a security group that allows access from your WordPress instances.
   - Availability Zone: Choose `No preference` for high availability.

6. **Database Options:**
   - Initial database name: `wordpress_db`.
   - Leave other settings as default.

7. **Create Database:**
   - Review your settings and click "Create database".

## Step 2: Configure Security Groups for RDS Instance

1. **Create a Security Group for RDS:**
   - Navigate to the VPC Dashboard.
   - Click on "Security Groups".
   - Click "Create security group".
   - Name: `wordpress-rds-sg`.
   - Description: `Security group for WordPress RDS instance`.
   - VPC: Select the VPC where your RDS instance is running.
   - Click "Create".

2. **Add Inbound Rules:**
   - Select `wordpress-rds-sg`.
   - Go to the "Inbound rules" tab and click "Edit inbound rules".
   - Click "Add rule".
   - Type: `MySQL/Aurora`.
   - Protocol: `TCP`.
   - Port range: `3306`.
   - Source: Select `Custom` and specify the security group used by your WordPress instances (e.g., `wordpress-sg`).
   - Click "Save rules".

3. **Associate Security Group with RDS Instance:**
   - Go to the RDS Dashboard.
   - Select your RDS instance (`wordpress-db`).
   - Click on the "Modify" button.
   - In the "Connectivity" section, under "VPC security groups", select `wordpress-rds-sg`.
   - Click "Continue" and then "Apply immediately".

## Step 3: Connect WordPress to the RDS Database

1. **Retrieve Database Endpoint:**
   - Go to the RDS Dashboard.
   - Select your RDS instance (`wordpress-db`).
   - Copy the "Endpoint" (e.g., `wordpress-db.xxxxxxx.us-west-2.rds.amazonaws.com`).

2. **Update WordPress Configuration:**
   - SSH into your WordPress server.
   - Open the `wp-config.php` file located in your WordPress directory.
   - Update the database configuration settings as follows:

   ```php
   /** The name of the database for WordPress */
   define('DB_NAME', 'wordpress_db');

   /** MySQL database username */
   define('DB_USER', 'admin');

   /** MySQL database password */
   define('DB_PASSWORD', 'your_password');

   /** MySQL hostname */
   define('DB_HOST', 'wordpress-db.xxxxxxx.us-west-2.rds.amazonaws.com');

   /** Database Charset to use in creating database tables. */
   define('DB_CHARSET', 'utf8mb4');

   /** The Database Collate type. Don't change this if in doubt. */
   define('DB_COLLATE', '');


