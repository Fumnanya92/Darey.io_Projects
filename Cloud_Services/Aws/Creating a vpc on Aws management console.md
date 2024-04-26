# Creating a vpc on Aws management console

## Task 1: Create a VPC

1. **Log in to the AWS Management Console:**
   - Open your web browser and go to [AWS Management Console](https://console.aws.amazon.com/).
   - Log in with your AWS account credentials.

2. **Navigate to the VPC service:**
   - Once logged in, click on the "Services" dropdown menu in the top-left corner.
   - Select "VPC" under the "Networking & Content Delivery" section. 

3. **Click on "Your VPCs" in the left navigation pane:**
   - In the left navigation pane, under "Virtual Private Cloud", click on "Your VPCs".

4. **Click the "Create VPC" button:**
   - On the "Your VPCs" page, click on the "Create VPC" button located at the top of the page.

5. **Fill in the details for your VPC:**
   - In the "Create VPC" wizard, you'll be prompted to fill in various details:
     - **Name tag:** Give your VPC a descriptive name.
     - **IPv4 CIDR block:** Specify the IPv4 CIDR block for your VPC (e.g., 10.0.0.0/16).
     - **IPv6 CIDR block (optional):** If you want to enable IPv6, you can specify an IPv6 CIDR block.
     - **Tenancy:** Choose whether you want the instances launched in this VPC to run on shared hardware (default) or dedicated hardware.
   - After filling in the details, click on the "Create" button to create your VPC.

