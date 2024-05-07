# VPC Peering with security group configuration 

## Task 1: Create Two VPCs

1. **Navigate to the VPC service**
   - In the AWS Management Console, search for "VPC".
   - Once in the VPC dashboard, locate and click on "Your VPCs" in the left navigation pane.

4. **Create VPC-A**
   - Click the "Create VPC" button.
   - Fill out the required information for VPC-A:
     - **Name tag:** Enter "VPC-A" as the name tag.
     - **IPv4 CIDR block:** Define an appropriate CIDR block for VPC-A.
     - Optionally, you can configure additional settings as needed.
   - Click "Create VPC" to create VPC-A.

5. **Create VPC-B**
   - Again, click the "Create VPC" button.
   - Fill out the required information for VPC-B:
     - **Name tag:** Enter "VPC-B" as the name tag.
     - **IPv4 CIDR block:** Define an appropriate CIDR block for VPC-B. Make sure it's different from VPC-A's CIDR block.
     - Optionally, configure additional settings as needed.
   - Click "Create VPC" to create VPC-B.

6. **Verify Creation**
   - After creating both VPCs, you should see them listed under "Your VPCs" in the VPC dashboard.

Congratulations! You have successfully created two VPCs named VPC-A and VPC-B.
