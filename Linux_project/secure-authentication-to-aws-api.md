# Mini Project - Setting Up Secure Authentication to AWS API

## Setting Up Secure Authentication to AWS API

Following the requirements detailed in the previous project, the initial step in crafting our script is to ensure we have the necessary AWS account setup for authentication and resource management in the cloud. This setup is crucial for enabling the script to create EC2 instances and S3 buckets efficiently. Here's how to proceed:

### 1. Create an IAM Role

Begin by establishing an IAM role that encapsulates the permissions required for the operations our script will perform.

1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to **IAM** (Identity and Access Management).
3. In the left navigation pane, click on **Roles**.
4. Click the **Create role** button.
5. Choose **AWS service** as the trusted entity type, and then select **EC2**.
6. Click **Next: Permissions**.
7. Skip the permissions for now by clicking **Next: Tags**.
8. Optionally add tags to help identify the role, then click **Next: Review**.
9. Enter a **Role name** (e.g., `automation_role`), and a description if desired.
10. Click **Create role**.

### 2. Create an IAM Policy

Design an IAM policy granting full access to both EC2 and S3 services. This policy ensures our script has the necessary permissions to manage these resources.

1. In the IAM dashboard, click on **Policies** in the left navigation pane.
2. Click the **Create policy** button.
3. Switch to the **JSON** tab.
4. Enter the following policy document:
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "ec2:*",
            "s3:*"
          ],
          "Resource": "*"
        }
      ]
    }
    ```
5. Click **Next: Tags**, optionally add tags, then click **Next: Review**.
6. Enter a **Name** for the policy (e.g., `EC2_S3_FullAccess`).
7. Click **Create policy**.
![screenshot of the policy created](https://github.com/Fumnanya92/Darey.io_Projects/assets/104866089/436fb667-cb49-4e76-ac86-65d3c517c3c3)


### 3. Create an IAM User

Instantiate an IAM user named `automation_user`. This user will serve as the primary entity our script uses to interact with AWS services.

1. In the IAM dashboard, click on **Users** in the left navigation pane.
2. Click the **Add user** button.
3. Enter `automation_user` as the **User name**.
4. Select **Programmatic access** as the access type.
5. Click **Next: Permissions**.

### 4. Assign the User to the IAM Role

Link the `automation_user` to the previously created IAM role to inherit its permissions. This step is vital for enabling the necessary access levels for our automation tasks.

1. In the **Set permissions** step, click **Next: Tags**.
2. Optionally add tags, then click **Next: Review**.
3. Review the details and click **Create user**.
4. Download the **.csv** file with the user's credentials or copy the **Access key ID** and **Secret access key**.

### 5. Attach the IAM Policy to the User

Ensure that the `automation_user` is explicitly granted the permissions defined in our IAM policy by attaching the policy directly to the user. This attachment solidifies the user's access to EC2 and S3 resources.

1. In the IAM dashboard, click on **Users**.
2. Select the `automation_user` from the list.
3. Click on the **Permissions** tab.
4. Click the **Add permissions** button.
5. Choose **Attach policies directly**.
6. Search for the `EC2_S3_FullAccess` policy created earlier and select it.
7. Click **Next: Review** and then **Add permissions**.

### 6. Create Programmatic Access Credentials

Generate programmatic access credentials - specifically, an access key ID and a secret access key for `automation_user`. These credentials are indispensable for authenticating our script with the AWS API through the Linux terminal, allowing it to create and manage cloud resources programmatically.

1. In the IAM dashboard, click on **Users**.
2. Select the `automation_user` from the list.
3. Click on the **Security credentials** tab.
4. Click the **Create access key** button.
5. Download the **.csv** file with the access key ID and secret access key or copy them directly.

With these steps completed, you now have a securely authenticated setup for interacting with AWS services through your script.

# Installing and Configuring the AWS CLI

After setting up your AWS account and creating the necessary IAM user and permissions, the next step involves installing the AWS Command Line Interface (CLI). The AWS CLI is a powerful tool that allows you to interact with AWS services directly from your terminal, enabling automation and simplification of AWS resource management.

## Step 1: Download AWS CLI

1. **Spin up an Ec2 instance**:
    - Launch an Ec2 instance and SSH into it. for this project I will be using Amozon Linux

2. **Download the AWS CLI installer**:
    - Use the `curl` command to download the AWS CLI installer. Run the following command in the terminal:
   **For Linux**
    ```sh
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    ```
   **For Windows**   
    ```sh
    curl "https://awscli.amazonaws.com/AWSCLIV2.msi" -o "AWSCLIV2.msi"
    ```

## Step 2: Install AWS CLI 
   **Linux**
    - Unzip awscliv2.zip and run the installer
    ```sh
    unzip awscliv2.zip
    sudo ./aws/install
    ```
    **Windows**
2. **Run the installer**:
   Use:
   ```
   msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
   ```
   Or
   **Open Windows Explorer**:
    - Navigate to the directory where you downloaded `AWSCLIV2.msi`.
    - Double-click the `AWSCLIV2.msi` file to start the installation process.
    - Follow the on-screen instructions to complete the installation.

## Step 3: Verify the Installation

1. **Check AWS CLI version**:
    - Confirm that the AWS CLI is installed correctly by checking its version. Run:
    ```sh
    aws --version
    ```
    - You should see output indicating the version of the AWS CLI installed, such as `aws-cli/2.x.x`.

## Step 4: Configure AWS CLI

1. **Run the configuration command**:
    - Configure the AWS CLI with your credentials and default region. Execute:
    ```sh
    aws configure
    ```

2. **Enter your credentials**:
    - You will be prompted to enter the following information:
        - **AWS Access Key ID**: Enter the access key ID from the credentials you generated for your IAM user.
        - **AWS Secret Access Key**: Enter the secret access key from the credentials you generated for your IAM user.
        - **Default region name**: Enter the desired default region (e.g., `us-west-2`).
        - **Default output format**: Enter the desired output format (e.g., `json`).

    Example configuration interaction:
    ```
    AWS Access Key ID [None]: YOUR_ACCESS_KEY_ID
    AWS Secret Access Key [None]: YOUR_SECRET_ACCESS_KEY
    Default region name [None]: us-west-2
    Default output format [None]: json
    ```
    ![image](https://github.com/Fumnanya92/Darey.io_Projects/assets/104866089/5e74a914-82a6-4243-bb3f-46d005c8e663)


## Step 5: Test the Configuration

1. **Run a simple AWS CLI command**:
    - To verify that the configuration is correct and the AWS CLI can communicate with your AWS service, run a simple command, such as listing your S3 buckets:
    ```sh
    aws s3 ls
    ```
    - Or try running a basic command to list all the AWS regions:
      ```
      aws ec2 describe-regions --output table
      ```
    - If your configuration is correct, you should see a list of your S3 buckets (if any exist) or the list of the regions
![image](https://github.com/Fumnanya92/Darey.io_Projects/assets/104866089/eafcd63a-49c4-4a0d-9d8c-c774f7cdf6de)


