# Setting up Amazon RDS with MySQL Engine

# Task 1: Create RDS Instance

1. **Log in to the AWS Management Console**
   - Open your web browser and navigate to the [AWS Management Console](https://aws.amazon.com/console/).
   - Enter your credentials (username and password) to log in.

2. **Navigate to the RDS Service**
   - Once logged in, find the search bar at the top of the console.
   - Type "RDS" and select "RDS" from the dropdown menu to navigate to the RDS service page.

3. **Create a Database**
   - On the RDS dashboard, click on the "Create database" button.

4. **Choose Easy create**
   - I the data "base creation method", selet Easy Create
     ![RDSEasycreate](https://github.com/Fumnanya92/Darey.io_Projects/assets/104866089/6c08fd02-9d14-46c3-9191-f7c770d1206f)


5. **Choose the MySQL Engine**
   - In the "Engine options" section, select the "MySQL" engine.

6. **Configure the RDS Instance Settings**
   - **DB Instance Identifier**: Enter a unique identifier for your database instance.
   - **Master Username**: Enter a master username for your database.
   - **Master Password**: Enter a master password and confirm it by re-entering.

7. **Additional Configuration (optional)**
   - Customize additional settings such as instance type, storage, VPC, security groups, backup, and maintenance preferences as needed.

8. **Review and Create**
   - Review all the settings you have configured.
   - Click on the "Create database" button to create your RDS instance.

9. **Wait for Instance Creation**
   - It may take a few minutes for AWS to create the RDS instance.
   - You can monitor the progress on the RDS dashboard.


# Task 2: Configure Security Group

1. **In the RDS Dashboard, Click on the Created RDS Instance**
   - Click on the identifier of the RDS instance you just created to view its details.

2. **In the 'Connectivity' Tab, Note the Security Group Associated with the RDS Instance**
   - Navigate to the 'Connectivity & security' tab of your RDS instance details page.
   - Under the "Security" section, find and note the security group ID associated with your RDS instance.

3. **Navigate to the EC2 Service and Update the Inbound Rules of the Security Group to Allow MySQL Traffic**
   - Go to the [EC2 dashboard](https://console.aws.amazon.com/ec2/).
   - In the left-hand menu, click on "Security Groups" under the "Network & Security" section.
   - Find the security group noted in the previous step and select it.
   - Click on the "Inbound rules" tab and then click on the "Edit inbound rules" button.
   - Add a new rule with the following details:
     - **Type**: MySQL/Aurora
     - **Protocol**: TCP
     - **Port Range**: 3306
     - **Source**: Custom (Enter the IP address range that you want to allow access, e.g., `0.0.0.0/0` for all IP addresses, though this is not recommended for production environments)
   - Click on the "Save rules" button to apply the changes.
   - 
# Task 3: Connect to RDS Instance

1. **Use a MySQL Client (e.g., MySQL Workbench) to Connect to the RDS Instance**

   - **Open MySQL Workbench**:
     - Launch MySQL Workbench on your computer.

   - **Create a New Connection**:
     - Click on the `+` icon next to "MySQL Connections" to create a new connection.

   - **Enter Connection Details**:
     - **Connection Name**: Enter a name for your connection (e.g., "AWS RDS MySQL").
     - **Hostname**: Enter the endpoint of your RDS instance. You can find this on the "Connectivity & security" tab of your RDS instance details page under "Endpoint & port".
     - **Port**: The default MySQL port is `3306`. Ensure this matches the port of your RDS instance.
     - **Username**: Enter the master username you specified when creating the RDS instance.
     - **Password**: Click on the "Store in Vault..." button (or equivalent) to enter and save your password securely.

   - **Test the Connection**:
     - Click on the "Test Connection" button to ensure all details are correct and the connection can be established. If successful, you should see a "Successfully made the MySQL connection" message.

   - **Save and Connect**:
     - Click on "OK" to save the connection settings.
     - Double-click on the connection you just created to connect to the RDS instance.


![RDSmysq](https://github.com/Fumnanya92/Darey.io_Projects/assets/104866089/48697bb7-dd6d-4cc8-b09c-3aab98d931cb)
