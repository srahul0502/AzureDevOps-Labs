# Deploying and Configuring a High-Availability Azure Load Balancer

## Notes to Instructor

### Common Challenges and Tips

1. **Network Configuration Issues:**
    - Students may forget to assign VMs to the same subnet or configure inbound port rules.
    - **Tip:** Verify that the VMs belong to the same virtual network and subnet.

2. **Health Probe Configuration:**
    - Students might not correctly configure health probes, resulting in unhealthy backend VMs.
    - **Tip:** Ensure correct protocol and port settings in the health probe (e.g., HTTP on port 80).

3. **Load Balancing Issues:**
    - Students might misconfigure load balancing rules, leading to traffic going to only one VM.
    - **Tip:** Confirm that both VMs are added to the backend pool, and session persistence is disabled.

## Submission Checklist

- Architecture diagram of VNet, Load Balancer, and backend pool connections
- **Screenshots:**
    - Virtual network and subnet configurations
    - Load Balancer settings (frontend, backend pool, and health probes)
    - Traffic distribution validation across backend VMs
- Detailed report with verification steps and traffic test results

### Sample Report Summary

**Verification Tips:**

- **Virtual Network:** Ensure the subnet IP range allows proper communication.
- **Backend Pool:** Confirm all VMs are in the backend pool and marked as "healthy."
- **Health Probes:** Validate success status for each backend VM.
- **Traffic Distribution:** Test with multiple refreshes to see responses from different VMs.

**Areas for Assistance:**

- Misconfigured health probes
- Backend pool not correctly associated
- Load balancing rule issues

## Solution:

### Step 1: Create a Virtual Network and Subnet

1. Go to the Azure Portal > Virtual Networks > Create Virtual Network.
    - **Name:** MyVNet
    - **Address Space:** 10.0.0.0/16
    - **Subnet Name:** MySubnet
    - **Subnet Address Range:** 10.0.0.0/24
    - Click **Review + Create** > **Create**.

    💡 Instructor Tip: Explain the purpose of subnets in isolating and managing network traffic within virtual networks.

### Step 2: Create Virtual Machines (VMs)

1. Navigate to Azure Portal > Virtual Machines > Create.
    - **Name:** VM1, VM2
    - **Region:** Select the same region as the virtual network
    - **Image:** Ubuntu Server 20.04 LTS
    - **Size:** Standard B1s or equivalent
    - **Authentication Type:** Password
    - **Virtual Network:** Select MyVNet
    - **Subnet:** Select MySubnet
    - **Public IP:** None
    - **Inbound Port Rules:** Allow HTTP (Port 80)
    - Click **Review + Create** > **Create**.

    💡 Instructor Tip: Explain why VMs should have no public IPs in this setup — traffic will be routed via the Load Balancer.

### Step 3: Install Web Servers on VMs

1. Connect to each VM via the Azure Cloud Shell or SSH.
2. Run the following commands to install Apache:

    ```sh
    sudo apt update
    sudo apt install apache2 -y
    echo "Welcome to VM1!" | sudo tee /var/www/html/index.html
    sudo systemctl start apache2
    ```

    Repeat the same commands on VM2, but change the message to "Welcome to VM2!"

    💡 Instructor Tip: Help students understand that these simple web servers will simulate real backend services for the Load Balancer.

### Step 4: Create an Azure Load Balancer

1. Go to Azure Portal > Load Balancers > Create.
    - **Resource Group:** Select an existing group or create a new one
    - **Name:** MyLoadBalancer
    - **Region:** Select the same region as the VMs
    - **Type:** Public
    - **Frontend IP Configuration:** Create a new public IP
    - Click **Review + Create** > **Create**.

### Step 5: Configure Backend Pool

1. Go to the Load Balancer resource > Backend Pools.
2. Click **Add Backend Pool:**
    - **Name:** MyBackendPool
    - **Virtual Network:** Select MyVNet
    - **Backend Pool Configuration:** Add VM1 and VM2.
    - Click **Add**.

    💡 Instructor Tip: Ensure students understand that backend pools are where the Load Balancer routes traffic.

### Step 6: Create Health Probes

1. Go to Load Balancer > Health Probes > Add a Health Probe.
    - **Name:** MyHealthProbe
    - **Protocol:** HTTP
    - **Port:** 80
    - **Interval:** 5 seconds
    - **Unhealthy Threshold:** 2

### Step 7: Configure Load Balancing Rules

1. Go to Load Balancer > Load Balancing Rules > Add a Rule.
    - **Name:** MyLBRule
    - **Frontend IP:** Select the public IP
    - **Backend Pool:** Select MyBackendPool
    - **Protocol:** TCP
    - **Port:** 80
    - **Session Persistence:** None
    - Click **Add**.

### Step 8: Verify Traffic Distribution

1. Copy the public IP of the Load Balancer.
2. Open a web browser and access the IP multiple times.
3. Verify that traffic is distributed across VM1 and VM2 by seeing alternating messages ("Welcome to VM1!" and "Welcome to VM2!").

    💡 Instructor Tip: Emphasize the importance of testing load distribution to ensure proper configurations.

## Submission Checklist

- Architecture diagram of the Load Balancer setup
- **Screenshots of:**
    - Virtual Network and subnet configuration
    - Load Balancer settings (frontend, backend pool, health probes)
    - Traffic distribution test results
- A report detailing:
    - Key configuration steps
    - Challenges faced and solutions

### Sample Report Summary

**Verification Tips:**

- Ensure backend VMs are marked "healthy" under the Load Balancer settings.
- Test traffic distribution by refreshing the browser multiple times.

**Common Errors:**

- Backend pool misconfiguration
- Incorrect health probe settings

## Additional Notes

- Encourage students to troubleshoot independently and ask questions when stuck.
- Highlight best practices for scalable network design and the importance of health probes in maintaining high availability.

## Solution Summary

1. **Create Virtual Network and Compute Resources:**
    - Deploy a virtual network and at least two virtual machines
    - Configure each VM to allow traffic on port 80

2. **Configure Load Balancer:**
    - Create a public-facing Load Balancer
    - Configure frontend IP and backend pool with the deployed VMs

3. **Configure Health Probes and Load Balancing Rules:**
    - Create a health probe on port 80
    - Set up a load balancing rule for HTTP traffic

4. **Test and Verify:**
    - Access the Load Balancer's public IP
    - Validate that traffic is distributed among backend VMs
