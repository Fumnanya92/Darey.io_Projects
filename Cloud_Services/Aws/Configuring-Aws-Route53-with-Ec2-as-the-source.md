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
  if you do not have a domain, purchase one here [link to purchase domain](https://www.godaddy.com/en-ie/domains)
- Choose the appropriate settings for your hosted zone:
  - **Type**: Select **Public Hosted Zone** for a publicly accessible domain.
- Click on the **Create hosted zone** button to proceed.

## Step 5: Note the Nameservers Provided by Route 53
- After creating the hosted zone, you will see a list of **Nameservers** provided by Route 53.
- Note down these nameservers as you will need to configure them with your domain registrar to point your domain to Route 53.

# Task 2: Configure DNS Records

## Step 1: Click on "Create Record Set" in the Hosted Zone You Created
- Click on the hosted zone to open it.
- Inside the hosted zone, click on the **Create Record Set** button.

## Step 2: Create an A Record Pointing to the Elastic IP Address of Your EC2 Instance
- In the **Create Record Set** form:
  - **Name**: Leave it blank to make it the apex record (e.g., example.com), or enter a subdomain if you want (e.g., www).
  - **Type**: Select **A - IPv4 address** from the dropdown menu.
  - **Alias**: Leave it as default (No).
  - **TTL (Seconds)**: Set the time-to-live value according to your preference (e.g., 30 seconds).
  - **Value**: Enter the Elastic IP address of your EC2 instance.
- Click on the **Create** button to add the A record to your hosted zone.

## Create a Record with Alias in AWS Route 53

## Step 1: Click on "Create Record Set"
- Inside the hosted zone, click on the **Create Record Set** button.

## Step 2: Configure the Alias Record
- In the **Create Record Set** form:
  - **Name**: Enter the subdomain for the record (e.g., `www`). Leave it blank if it's for the root domain (e.g., example.com).
  - **Type**: Select the record type from the dropdown menu, such as **A - IPv4 address** or **AAAA - IPv6 address**.
  - **Alias**: Select **Yes**.
  - **Route traffic to**: Select **Alias to another record in this zone**
  - **Alias Target**: Click on the text box to see a list of AWS resources. Select the appropriate resource (e.g., an Elastic Load Balancer, CloudFront distribution, or another Route 53 record).
  - **Routing Policy**: Choose the routing policy you want to apply (e.g., Simple, Weighted, Latency, Failover, Geolocation, Multi-value answer, or Geoproximity).
  - **Evaluate Target Health**: Select **Yes** if you want Route 53 to evaluate the health of the selected endpoint.

## Step 5: Create the Record
- Click on the **Create** button to add the alias record to your hosted zone.

  # Task 4: Copy the Name Servers from AWS Route 53 and Paste Them into GoDaddy

## Step 1: Retrieve Name Servers from AWS Route 53
- Open the AWS Management Console.
- Navigate to the **Route 53** service.
- In the Route 53 dashboard, locate the hosted zone you created.
- Click on the hosted zone to open it.
- In the **Hosted Zone Details** section, you will see a list of **Name Servers**.
- Note down the values of the name servers (there are typically four).

## Step 2: Log in to Your GoDaddy Account
## Step 3: Navigate to Your Domain Settings
## Step 4: Update the Name Servers

# Task 4: Test DNS Resolution

## Step 1: Open a Web Browser and Enter Your Domain Name
- Open any web browser on your computer or device.

## Step 2: Verify That the Browser Resolves the Domain to the IP Address of Your EC2 Instance
- In the address bar of the web browser, enter your domain name (e.g., example.com).
- Press Enter to navigate to the website.
- Wait for the page to load.
- Verify that the website loads successfully.
- Check the URL displayed in the browser's address bar to confirm that it matches the domain name you entered.
- If the website loads and the URL matches your domain name, it indicates that DNS resolution is successful, and the domain is correctly pointing to the IP address of your EC2 instance.





