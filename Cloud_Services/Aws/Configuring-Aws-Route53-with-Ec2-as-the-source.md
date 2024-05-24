# Configuring Aws Route53 with Ec2 as the source

# Task 1: Create Hosted Zone

## Step 1: Log in to the AWS Management Console
- Open your web browser and go to the [AWS Management Console](https://aws.amazon.com/console/).
- Enter your AWS account credentials to log in.

## Step 2: Navigate to the Route 53 Service
- Once logged in, locate the **Services** menu at the top of the page.
- From the drop-down menu, select **Route 53** under the **Networking & Content Delivery** category.

## Step 3: Click on "Create Hosted Zone"
- In the Route 53 dashboard, find the **Hosted zones** section.
- Click on the **Create hosted zone** button.

## Step 4: Enter Your Domain Name and Configure the Hosted Zone Settings
- In the **Create Hosted Zone** form, enter your domain name in the **Domain Name** field.
- Choose the appropriate settings for your hosted zone:
  - **Type**: Select **Public Hosted Zone** for a publicly accessible domain or **Private Hosted Zone** for a domain only accessible within your VPC.
  - Optionally, add a comment to describe the hosted zone.
- Click on the **Create hosted zone** button to proceed.

## Step 5: Note the Nameservers Provided by Route 53
- After creating the hosted zone, you will see a list of **Nameservers** provided by Route 53.
- Note down these nameservers as you will need to configure them with your domain registrar to point your domain to Route 53.

