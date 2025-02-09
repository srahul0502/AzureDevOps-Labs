# Lab Title: Secure Network Traffic with Azure Firewall

## Lab Overview

This lab guides you through the process of provisioning, configuring, and testing an Azure Firewall. By the end of this lab, you will gain a clear understanding of Azure Firewall features and how to secure virtual network resources.

## Pre-requisites

- An active Azure subscription.
- Basic understanding of Azure Networking concepts.
- Azure CLI or access to the Azure Portal.
- Permissions to create and manage network resources.

## Learning Objectives

By completing this lab, you will:

- Learn how to provision and configure an Azure Firewall.

- Gain practical skills in setting up and managing virtual network security.

- Understand how to create and apply application and network rules.

- Test and validate firewall functionality by controlling access to resources.

## Description

Azure Firewall is a cloud-native and intelligent network firewall security service that provides threat protection for your cloud workloads running in Azure. This lab will walk you through deploying and configuring an Azure Firewall to secure resources within a virtual network.

## TASKS

### Task 1: Create a Resource Group

**Objective:** Create a dedicated resource group to manage all related Azure resources for this lab.

**Instructions:**

1. Navigate to the Azure Portal.
2. In the search bar at the top, type **Resource groups** and click the search result.
3. Click the **+ Create** button.
4. Under Project details, select your Azure subscription.
5. Under Instance details:
    - Enter a unique name for the resource group (e.g., `AzureFirewallLabRG`).
    - Select the desired Region from the dropdown.
6. Click **Review + Create**, then click **Create** once validation is complete.

**Verification:**

- Navigate back to the **Resource groups** section and confirm that the newly created resource group appears in the list.
- Verify the correct location and name.

### Task 2: Create a Virtual Network and Subnets

**Objective:** Set up a virtual network with required subnets to host the firewall and backend resources.

**Instructions:**

1. In the Azure Portal, search for **Virtual networks** and select it from the results.

2. Click **+ Create**.

3. Select the previously created resource group.

4. Under **Instance Details**, provide:
    - **Name**: `AzureFirewallVNet`
    - **Region**: Select the same region as the resource group

Note: Make sure to create 3 Address Space `10.0.1.0/24`,`10.0.2.0/24`,`10.0.3.0/24`

5. Under **IP Addresses**, click **+ Add Subnet**:
    - **Subnet Purpose**: Select `Azure Firewall`
    - **Name**: This will automatically become `AzureFirewallSubnet` (cannot be changed due to system constraints)
    - **Address range (CIDR block)**: `10.0.1.0/24`

6. Click **Add**.

7. Click **+ Add Subnet** again for Firewall Manager subnet:
    - **Subnet Purpose**:v select `FirewallManagementSubnet`
    - **Name**: `AzureFirewallManagementSubnet`
    - **Address range (CIDR block)**: `10.0.2.0/24`
  
8. Click **Add**.

9.  Click **+ Add Subnet** again for backend subnet:
    - **Subnet Purpose**: Leave it as `None` (default)
    - **Name**: `BackendSubnet`
    - **Address range (CIDR block)**: `10.0.3.0/24`

10. Click **Add**.

11. Click **Review + Create**, then **Create**.


**Verification:**

- Navigate to the **Virtual networks** section.
- Open the `AzureFirewallVNet` resource and verify that both `AzureFirewallSubnet`,`BackendSubnet`,`FirewallManager` are listed under **Subnets**.

### Task 3: Deploy the Azure Firewall

**Objective:** Deploy an Azure Firewall in the newly created virtual network.

**Instructions:**

1. In the Azure Portal, search for **Azure Firewall** and select it.
2. Click **+ Create**.
3. Select the correct Subscription and Resource Group (`AzureFirewallLabRG`).
4. Provide the following details under Instance details:
    - **Name:** `MyAzureFirewall`
    - **Region:** Select the same region as the virtual network.
5. Under Firewall management:
    - Select **Use Firewall Policy**.
    - Click **Create new** if prompted.
6. Under Virtual Network:
    - Select `AzureFirewallVNet`.
    - Select the subnet `AzureFirewallSubnet`.
7. Under Public IP Configuration:
    - Select **Add new public IP address**.
    - Provide a name for the IP resource (e.g., `MyFirewallPublicIP`).
8. Click **Review + Create**, then **Create**.

**Verification:**

- Navigate to the **Azure Firewalls** section and ensure the firewall status is Running.
- Verify the associated public IP resource under **IP Configurations**.

## Task 4: Configure Firewall Rules

**Objective:** Set up firewall rules to manage network traffic.

### Instructions:

1. Go to **Azure Portal** > Navigate to your deployed firewall (MyAzureFirewall).

2. On the left panel, select **Firewall Policy** (if prompted to create or attach a policy, do that).

3. Click **Rules Collections** under **Settings**. You should see options to create:
    - Application Rule Collection
    - Network Rule Collection

#### Step 1: Adding Application Rule Collection

1. Select **Application Rule Collection** > **+ Add Rule Collection**.

2. Fill in the following:
    - **Name:** `AppRuleCollection1`
    - **Priority:** 100
    - **Action:** Allow

3. In the **Rules** section, provide these details:
    - **Name:** `AllowMicrosoftAccess`
    - **Source:** `10.0.3.0/24`
    - **Protocol:** Http/80, Https/443
    - **Target FQDNs:** `www.microsoft.com`

4. Click **Add**.
   
   ![alt text](<Screenshot 2025-02-09 104639-rulecollection1.png>)

#### Step 2: Adding Network Rule Collection

1. Select **Network Rule Collection** > **+ Add Rule Collection**.

2. Fill in the following details:
    - **Name:** `NetRuleCollection1`
    - **Priority:** 200
    - **Action:** Allow

3. In the **Rules** section, provide:
    - **Name:** `AllowAllTraffic`
    - **Source Address:** `10.0.3.0/24`
    - **Destination Address:** `*` (wildcard for any destination)
    - **Destination Ports:** 80, 443
    - **Destination Type:** IPAddress
    - **Protocol:** TCP

4. Click **Add**.
   
    ![alt text](<Screenshot 2025-02-09 -networkconnection.png>)

### Verification:

1. Navigate to the **Rules Collection Groups** section and ensure both rule collections (`AppRuleCollection1`, `NetRuleCollection1`) are present.

2. Check that the rules (`AllowMicrosoftAccess`, `AllowAllTraffic`) are configured correctly with the specified sources, destinations, and protocols.

3. Test by initiating traffic from a virtual machine in the BackendSubnet. Ensure access to `www.microsoft.com` is allowed, while other sites are restricted.   

### Task 5: Test Firewall Rules

**Objective:** Validate the functionality of firewall rules by testing network traffic.

**Instructions:**

1. Deploy a virtual machine (VM) in the `BackendSubnet`.
    - In the Azure Portal, search for **Virtual machines** and click **+ Create**.
    - Select the resource group `AzureFirewallLabRG`.
    - Provide the following details under Instance details:
        - **Name:** `TestVM`
        - **Region:** Select the same region as other resources.
        - **Image:** Select Windows Server 2019 or Ubuntu 20.04.
        - **Size:** Select a suitable size (e.g., `Standard_B1s`).
    - Under Administrator Account:
        - Provide a username and password.
    - Under Networking:
        - Select `AzureFirewallVNet`.
        - Select `BackendSubnet`.
        - Enable public IP for access.
    - Click **Review + Create**, then **Create**.
2. Once the VM is deployed, connect to it via RDP (for Windows) or SSH (for Linux).
3. Open a browser inside the VM and navigate to `www.microsoft.com`.
    - Confirm that the website loads successfully.
    ![alt text](<Screenshot 2025-02-09 110144successfulconnection.png>)
4. Attempt to access a blocked website (e.g., `www.blockedexample.com`).
   
   ![alt text](<Screenshot 2025-02-09 110946notfound.png>)

**Verification:**

- Ensure that access to `www.microsoft.com` is allowed.
- Confirm that access to the blocked website is denied.

### Task 6: Clean Up Resources

**Objective:** Remove all resources to avoid unnecessary charges.

**Instructions:**

1. Navigate to the **Resource groups** blade.
2. Select the resource group `AzureFirewallLabRG`.
3. Click **Delete resource group**.
4. Confirm the deletion by typing the resource group name and clicking **Delete**.

**Verification:**

- Ensure that the resource group and its resources are deleted.
- Verify that no remnants of the deployment remain.

---

## Submission Guidelines

- Provide screenshots of the deployed firewall, rule configuration, and successful/failed traffic tests.
- Document the steps followed and any challenges faced.

## Additional Resources

- [Azure Firewall Documentation](https://docs.microsoft.com/en-us/azure/firewall/)
- [Azure Networking Concepts](https://docs.microsoft.com/en-us/azure/virtual-network/)
