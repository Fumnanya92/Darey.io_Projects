# S3 Versioning and Replication

**Amazon S3 Cross Region Replication enables replicating objects from a source bucket to a destination bucket in a different AWS region. This can help with compliance, reduce latency, and improve operational efficiency.**


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
   ![screenshot of bucket created](image/s3versioning1.png)

## Task 2: Enable Versioning

## Step 1: Navigate to the "Versioning" section in S3 bucket properties
- Find and click on "s3versioning1".
- Once inside the bucket, locate and click on the "Properties" tab.
  ![screenshot of properties](image/s3versioningproperties.png)

## Step 2: Enable versioning for the S3 bucket
- Scroll down or navigate to the "bucket Versioning" section.
- Click on the option to enable versioning for the bucket.

## Step 3: Confirm versioning configuration
- After enabling versioning, AWS will display a confirmation dialog or message.
- Review the information to ensure that versioning has been successfully enabled for the S3 bucket.
  ![screenshot of versioning enabled](image/s3versioningenabled.png)


## Task 3: Configure Cross-Region Replication

## Step 1: Navigate to the "Management" tab in S3 bucket properties
- Log in to the AWS Management Console and navigate to the S3 service.
- Find and click on the name of the S3 bucket you want to configure cross-region replication for.
- Inside the bucket, locate and click on the "Management" tab. This tab contains various management settings for the bucket.

## Step 2: Click on "Replication" and configure cross-region replication
- Within the "Management" tab, look for the "Replication" option and click on it.
- You'll be presented with the configuration settings for cross-region replication.
- Here's an example configuration:
  - **Source Region:** Select the region where your S3 bucket is located.
  - **Destination Region:** Choose another region where you want to replicate the data.
  - **IAM Role:** Create a new IAM role or select an existing IAM role that grants permission for replication. This role should have permissions to read from the source bucket and write to the destination bucket.
  
## Step 3: Configure replication rules (if needed)
- Depending on your requirements, you may need to configure replication rules to specify which objects should be replicated and any additional settings.
- These rules can include filters based on object tags, prefixes, or other criteria.
- Follow the prompts to configure replication rules as needed for your use case.

## Step 4: Review and save the configuration
- After configuring cross-region replication settings and any replication rules, review the settings to ensure they are correct.
- Once you're satisfied with the configuration, click on the appropriate button to save or apply the changes.

## Step 5: Verify replication configuration
- After saving the replication configuration, AWS will begin replicating objects from the source bucket to the destination bucket in the specified regions.
- You can monitor the replication status and progress in the S3 Management Console.
- Verify that replication is working as expected by checking the destination bucket for replicated objects.

Congratulations! You have successfully configured cross-region replication for the specified S3 bucket, ensuring that data is replicated to another region for redundancy or compliance purposes.



