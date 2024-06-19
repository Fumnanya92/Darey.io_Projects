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
![screenshot of the policy created](![image](https://github.com/Fumnanya92/Darey.io_Projects/assets/104866089/436fb667-cb49-4e76-ac86-65d3c517c3c3)
)

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
