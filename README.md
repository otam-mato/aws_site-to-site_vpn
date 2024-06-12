# AWS Site-To-Site VPN

### Setting up an AWS VPN to an on-premises network involves creating a Virtual Private Gateway on AWS, configuring a Customer Gateway on your on-premises network, and setting up the VPN connection between the two.

### Step 1: Set Up a Virtual Private Gateway

1. **Login to AWS Management Console:**
   - Go to the AWS Management Console and log in with your credentials.

2. **Navigate to VPC:**
   - In the services menu, select "VPC."

3. **Create a Virtual Private Gateway:**
   - On the left-hand menu, click on "Virtual Private Gateways."
   - Click the "Create Virtual Private Gateway" button.
   - Provide a name for your gateway, and select the ASN (Autonomous System Number) or leave it as default.
   - Click "Create Virtual Private Gateway."
   ![image](https://hackmd.io/_uploads/BkqRB7wrA.png)

4. **Attach the Virtual Private Gateway to Your VPC:**
   - Once created, select the Virtual Private Gateway.
   - Click on "Actions" and select "Attach to VPC."
   - Choose the VPC you want to attach it to and click "Attach."
   ![image](https://hackmd.io/_uploads/H1gMvXwHC.png)


### Step 2: Configure the Customer Gateway

1. **Obtain Your On-Premises Public IP:**
   - Make sure you have the static public IP address of your on-premises router or firewall that will connect to the VPN.

2. **Create a Customer Gateway:**
   - In the VPC dashboard, click on "Customer Gateways" on the left-hand menu.
   - Click the "Create Customer Gateway" button.
   - Provide a name for the Customer Gateway.
   - Enter the public IP address of your on-premises router or firewall.
   - Select the BGP ASN (if using dynamic routing), or leave it blank for static routing.
   - Click "Create Customer Gateway."
   ![image](https://hackmd.io/_uploads/HJvNHmPHC.png)

### Step 3: Set Up the VPN Connection

1. **Create a VPN Connection:**
   - In the VPC dashboard, click on "VPN Connections" on the left-hand menu.
   - Click the "Create VPN Connection" button.
   - Provide a name for the VPN connection.
   - Select the Virtual Private Gateway you created earlier.
   - Select the Customer Gateway you created earlier.
   - Choose the routing type (Static or Dynamic).
   - If static, enter the prefixes CIDR blocks for your on-premises network and VPC.
   - Click "Create VPN Connection."
   ![image](https://hackmd.io/_uploads/S1UiuXDB0.png)


2. **Download the VPN Configuration:**
   - Once the VPN connection is created, select it.
   - Click on "Download Configuration."
   - Choose the appropriate vendor and platform for your on-premises device and download the configuration file.

### Step 4: Configure Your On-Premises Device

1. **Use the Configuration File:**
   - Open the downloaded configuration file. It contains the necessary parameters and commands to configure your on-premises device.
   ![image](https://hackmd.io/_uploads/rkaiKXDSC.png)


2. **Configure Your On-Premises Router/Firewall:**
   - Apply the configuration settings from the downloaded file to your on-premises router or firewall.
   - This will typically involve setting up IKE and IPsec parameters, defining the remote peer IP (the AWS VPN gateway), and configuring the pre-shared key.

### Step 5: Configure Route Tables

1. **Update VPC Route Table:**
   - Go to "Route Tables" in the VPC dashboard.
   - Select the route table associated with your VPC.
   - Add a new route, with the destination being your on-premises network CIDR block and the target being the Virtual Private Gateway.
   ![image](https://hackmd.io/_uploads/rJLNo7wHC.png)
   ![image](https://hackmd.io/_uploads/BJ1U3mvHC.png)



2. **Update On-Premises Routing:**
   - Ensure that your on-premises network has routes configured to send traffic destined for the AWS VPC through the VPN tunnel.

### Step 6: Test the VPN Connection

1. **Check the VPN Status on AWS:**
   - In the VPC dashboard, go to "VPN Connections."
   - Select your VPN connection and check the status of the tunnels. They should be in the "UP" state if configured correctly.
   ![image](https://hackmd.io/_uploads/Hy58aQvrC.png)


2. **Verify Connectivity:**
   - From your on-premises network, try to ping or access resources in the AWS VPC to verify the VPN connection is working.
   - Ensure that routing is correctly set up on both sides so that traffic can flow between the on-premises network and the VPC.



### Additional Considerations

- **Network ACLs and Security Groups:**
  - Ensure that your network ACLs and security groups allow the necessary traffic to and from your on-premises network.

- **Monitoring and Logging:**
  - Set up CloudWatch and VPC Flow Logs to monitor and log VPN traffic for troubleshooting and analysis.
