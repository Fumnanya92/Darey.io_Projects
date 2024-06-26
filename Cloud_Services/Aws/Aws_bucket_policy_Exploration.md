# Aws bucket policy Exploration 

### Purpose:

In this mini project, you will work with Amazon S3 bucket policies to control access to your S3 buckets. The project will guide you through creating a simple S3 bucket, defining a policy to manage access permissions, and testing the policy by uploading and retrieving objects.

1. **Log in to the AWS Management Console.**
   ```
   Open your web browser and go to (https://aws.amazon.com/console/).
   Enter your username and password.
   Click "Sign In".
   ```
2. **Navigate to the S3 service:**
   ```
   Once logged in, at the top of the AWS Management Console, you'll see a search bar. 
   Type in "S3" and select "Amazon S3" from the search results.
   ```

3. **Click the "Create bucket" button:**
   ```
   In the Amazon S3 dashboard, click the "Create bucket" button.
   This will open a new window where you can configure your bucket.
   ```
   ![screenshot of the create bucket button](image/Create_bucket.png)

4. **Follow the prompts to configure the new S3 bucket:**
   
   **Bucket Name and Region:**
   ```
   Enter a unique bucket name.
   Select the region for your bucket.
   ```

   **Configure Options (Optional):**
   `Set up options such as versioning, logging, and tags as needed.`
   
   **Set Permissions:**
  ` Define who can access the bucket and the objects inside it.`
   
   **Review:**
   `Double-check all the configurations you've made.`
   
   **Create Bucket:**
   `Click the "Create bucket" button to finalize the process.`
   ![screenshot of creating bucket button](image/Creating_bucket.png)

5. **Confirmation:**
   Once the bucket is created, you'll see a confirmation message.
   You can now start uploading files to your new S3 bucket!
   ![screenshot of bucket created](image/bucket_created.png)


6. **Upload a test object to your S3 bucket:**
   ```
   Open the bucket you created.
   Create a folder
   Open the folder
   Click the "Upload" button.
   Select a test file from your local computer and upload it to the bucket.
   ```
   ![screenshot of the folder button](image/Create_folder.png)

7. **Create a new JSON-formatted bucket policy in the AWS Management Console**
   ```
   {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::dareyioproject/*",
            "Condition": {
                "IpAddress": {
                    "aws:SourceIp": "102.88.70.98"
                }
            }
        }
    ]
   }
   ```

8. **Apply the policy to your S3 bucket**
   ![screenshot of Json bucket policy](image/json_policy.png)
9. **Retrieve the object from various scenarios:**
   - **Use an allowed IP address:**
     - Access the object from a network with an IP address that you have allowed in the bucket policy or IAM policy.
       in my case 102.88.70.98
     - You should be able to retrieve the object successfully.

   - **Use a restricted IP address:**
     - Access the object from a network with an IP address that is restricted in the bucket policy or IAM policy.
     - You should receive an access denied error or a similar message indicating the restriction.

   - **Use different IAM users:**
     - Attempt to access the object using each IAM user's credentials.
     - Verify the access based on the permissions assigned to each IAM user.
     - 
4. **Testing Complete:**
   - After testing with various scenarios, I have observed the access control configurations of my S3 bucket.
   - This helps ensure that my S3 bucket is configured securely according to my access requirements.



