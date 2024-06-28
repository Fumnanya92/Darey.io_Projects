# SHELL SCRIPTING FOR AWS MANAGEMENT

# Capstone Project: Shell Script for AWS IAM Management

## Project Scenario
Linux Adm and Shell

Datawise Solutions requires efficient management of AWS Identity and Access Management (IAM) resources. The company is expanding its team and needs to onboard five new employees to access AWS resources securely.

## Purpose
In this capstone project, you will extend your shell scripting capabilities by creating more functions that extend the `aws_cloud_manager.sh` script.

## Evaluation Criteria

### 1. Script Enhancement (30 points)

#### 1.1. CentOS Support (15 points)

- Successful extension of the provided script to include support for CentOS.
- Proper modification of functions and conditional statements for CentOS compatibility.

#### 1.2. Script Modularity (15 points)

- Clear organization of the script with modular functions for package installation, service management, and artifact deployment.
- Effective use of functions for different Linux distributions.

### 2. Infrastructure Setup (30 points)

#### 2.1. EC2 Instance Launch (15 points)

- Proper launch of EC2 instances with Amazon Linux, Ubuntu, and CentOS.
- Configuration of instance attributes such as instance type, security groups, and key pairs.

#### 2.2. Security Measures (15 points)

- Appropriate configuration of security groups to ensure optimal security measures.
- Proper setup of key pairs for secure remote access.

### 3. Remote Execution and Deployment (30 points)

#### 3.1. Script Upload (10 points)

- Successful upload of the enhanced script to a centralized server.
- Secure handling of the script to prevent unauthorized access.

#### 3.2. Remote Execution (10 points)

- Proper execution of the script on each instance remotely.
- Handling of dependencies and adjustments for different distributions.

#### 3.3. Apache Deployment (5 points)

- Successful deployment of the Apache web server on each instance.
- Verification of the Apache service status.

#### 3.4. Sample Web Application Deployment (5 points)

- Successful deployment of a sample web application on each instance.
- Verification of web application accessibility.

### 4. Documentation (20 points)

#### 4.1. Remote Deployment Process (7 points)

- Comprehensive documentation detailing the entire remote deployment process.
- Clear step-by-step instructions for each task, including script enhancement, infrastructure setup, and remote execution.

#### 4.2. Configuration Details (5 points)

- Detailed documentation of configurations made during infrastructure setup.
- Explanation of security measures implemented.

#### 4.3. Challenges and Solutions (5 points)

- Identification and documentation of challenges encountered during the project.
- Clear presentation of solutions implemented to overcome challenges.

#### 4.4. Key Findings and Insights (3 points)

- A brief report summarizing key findings and insights gained from the project.
- Reflection on the significance of deploying across multiple Linux distributions for system reliability.

### 5. Script Link Submission (20 points)

#### 5.1. Link Submission (20 points)

- Submission of a link to the script used for remote execution.
- Verification that the link provides access to the enhanced script with CentOS support.

## Objectives

1. **Script Enhancement:**
    - Extend the provided script to include IAM management.
    
    ```bash
    #!/bin/bash

    # Environment variables
    ENVIRONMENT=$1

    check_num_of_args() {
    # Checking the number of arguments
    if [ "$#" -ne 0 ]; then
        echo "Usage: $0 <environment>"
        exit 1
    fi
    }

    activate_infra_environment() {
    # Acting based on the argument value
    if [ "$ENVIRONMENT" == "local" ]; then
      echo "Running script for Local Environment..."
    elif [ "$ENVIRONMENT" == "testing" ]; then
      echo "Running script for Testing Environment..."
    elif [ "$ENVIRONMENT" == "production" ]; then
      echo "Running script for Production Environment..."
    else
      echo "Invalid environment specified. Please use 'local', 'testing', or 'production'."
      exit 2
    fi
    }

    # Function to check if AWS CLI is installed
    check_aws_cli() {
        if ! command -v aws &> /dev/null; then
            echo "AWS CLI is not installed. Please install it before proceeding."
            return 1
        fi
    }

    # Function to check if AWS profile is set
    check_aws_profile() {
        if [ -z "$AWS_PROFILE" ]; then
            echo "AWS profile environment variable is not set."
            return 1
        fi
    }

    # Function to create EC2 Instances
    create_ec2_instances() {

        # Specify the parameters for the EC2 instances
        instance_type="t2.micro"
        ami_id="ami-0cd59ecaf368e5ccf"  
        count=2  # Number of instances to create
        region="eu-west-2" # Region to create cloud resources
        
        # Create the EC2 instances
        aws ec2 run-instances \
            --image-id "$ami_id" \
            --instance-type "$instance_type" \
            --count $count
            --key-name MyKeyPair
            
        # Check if the EC2 instances were created successfully
        if [ $? -eq 0 ]; then
            echo "EC2 instances created successfully."
        else
            echo "Failed to create EC2 instances."
        fi
    }

    # Function to create S3 buckets for different departments
    create_s3_buckets() {
        # Define a company name as prefix
        company="datawise"
        # Array of department names
        departments=("Marketing" "Sales" "HR" "Operations" "Media")
        
        # Loop through the array and create S3 buckets for each department
        for department in "${departments[@]}"; do
            bucket_name="${company}-${department}-Data-Bucket"
            # Create S3 bucket using AWS CLI
            aws s3api create-bucket --bucket "$bucket_name" --region your-region
            if [ $? -eq 0 ]; then
                echo "S3 bucket '$bucket_name' created successfully."
            else
                echo "Failed to create S3 bucket '$bucket_name'."
            fi
        done
    }

    check_num_of_args
    activate_infra_environment
    check_aws_cli
    check_aws_profile
    create_ec2_instances
    create_s3_buckets
    ```

2. **Define IAM User Names Array:**
    - Store the names of the five IAM users in an array for easy iteration during user creation.

    ```bash
    # Define IAM User Names Array
    iam_users=("user1" "user2" "user3" "user4" "user5")
    ```

3. **Create IAM Users:**
    - Iterate through the IAM user names array and create IAM users for each employee using AWS CLI commands.

    ```bash
    create_iam_users() {
        for user in "${iam_users[@]}"; do
            aws iam create-user --user-name "$user"
            if [ $? -eq 0 ]; then
                echo "IAM user '$user' created successfully."
            else
                echo "Failed to create IAM user '$user'."
            fi
        done
    }
    ```
    ![image](https://github.com/Fumnanya92/Darey.io_Projects/assets/104866089/0134cbd8-1d7c-4236-9c93-de428358bbcc)


4. **Create IAM Group:**
    - Define a function to create an IAM group named "admin" using the AWS CLI.

    ```bash
    create_iam_group() {
        aws iam create-group --group-name admin
        if [ $? -eq 0 ]; then
            echo "IAM group 'admin' created successfully."
        else
            echo "Failed to create IAM group 'admin'."
        fi
    }
    ```
    ![image](https://github.com/Fumnanya92/Darey.io_Projects/assets/104866089/699b86ad-6c37-49e2-be25-24f76924b145)


5. **Attach Administrative Policy to Group:**
    - Attach an AWS-managed administrative policy (e.g., "AdministratorAccess") to the "admin" group to grant administrative privileges.

    ```bash
    attach_admin_policy_to_group() {
        aws iam attach-group-policy --group-name admin --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
        if [ $? -eq 0 ]; then
            echo "Administrative policy attached to group 'admin' successfully."
        else
            echo "Failed to attach policy to group 'admin'."
        fi
    }
    ```

    ![Uploading image.png…]()


6. **Assign Users to Group:**
    - Iterate through the array of IAM user names and assign each user to the "admin" group using AWS CLI commands.

    ```bash
    assign_users_to_group() {
        for user in "${iam_users[@]}"; do
            aws iam add-user-to-group --user-name "$user" --group-name admin
            if [ $? -eq 0 ]; then
                echo "IAM user '$user' added to group 'admin' successfully."
            else
                echo "Failed to add IAM user '$user' to group 'admin'."
            fi
        done
    }
    ```

## Project Deliverables

1. Comprehensive documentation detailing your entire thought process in developing the script.
2. Link to the script used for remote execution.

## Remote Deployment Process

### Step-by-Step Instructions

1. **Script Enhancement:**
    - Enhance the provided script to include IAM management.
    - Ensure the script supports multiple Linux distributions including CentOS.

2. **Infrastructure Setup:**
    - Launch EC2 instances with Amazon Linux, Ubuntu, and CentOS.
    - Configure instance attributes and security groups.

3. **Remote Execution and Deployment:**
    - Upload the enhanced script to a centralized server.
    - Execute the script remotely on each instance.
    - Deploy the Apache web server and a sample web application.

4. **Configuration Details:**
    - Document configurations made during the infrastructure setup.
    - Explain the
