# S3 bucket policy for CloudFront Access

Purpose:

In this mini project, you will configure an S3 bucket policy that allows access only from a specific CloudFront distribution. This ensures that your S3 content is securely served through CloudFront, and direct access to the S3 bucket is restricted


1. **Log in to the AWS Management Console.**
   ```
   Open your web browser and go to (https://aws.amazon.com/console/).
   Enter your username and password.
   Click "Sign In".
   ```
2. **Navigate to the S3 service:**
   ```
   Once logged in, on the search tab at the top of the AWS Management Console,
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
   
   **Review:**
   
   **Create Bucket:**
   `Click the "Create bucket" button to finalize the process.`
   ![screenshot of creating bucket button](image/Creating_bucket.png)

5. **Confirmation:**
   Once the bucket is created, you'll see a confirmation message.
   You can now start uploading files to your new S3 bucket!
   ![screenshot of bucket created](image/cloudfronts3.png)
   

   ## Task 2: Create a CloudFront Distribution

1. **Navigate to CloudFront Service:**
   - Go to the CloudFront service.

2. **Initiate Creation of Distribution:**
   - On the CloudFront dashboard, locate and click the "Create Distribution" button.
     ![screenshot of create distrubution](image/cloudfrontdistribution.png)
   
4. **Configure Distribution Settings:**
   - **Origin Settings:**
     - Choose your S3 bucket as the origin.
     - `use website endpoint`
     ![screenshot of create origin](image/cloudfrontorigin.png)

   - **Default Cache Behavior Settings:**
     - Adjust cache behaviors according to your requirements (e.g., cache duration, query string handling).
   - **Distribution Settings:**
     - Specify additional settings such as logging, SSL certificate, supported HTTP versions, etc.
   
5. **Optional Settings Configuration:**
   - **Cache Behavior Settings:**
     - Configure cache behaviors for specific paths or patterns, if needed.
   - **Distribution Settings:**
     - Adjust default settings such as price class, IPv6 support, and comment.
   - **Additional Features:**
     - Enable features like Lambda@Edge, field-level encryption, etc., as per your requirements.

6. **Review and Create:**
   - After configuring the settings, review your choices to ensure everything is set up correctly.
   - Click the "Create Distribution" button to initiate the creation process.

7. **Wait for Distribution Deployment:**
   - CloudFront distributions typically take some time to deploy. Monitor the status in the CloudFront dashboard until it shows as deployed.

8. **Verify Configuration:**
   - Once deployed, verify the CloudFront distribution's settings and functionality by accessing the provided domain name or endpoint.



   
