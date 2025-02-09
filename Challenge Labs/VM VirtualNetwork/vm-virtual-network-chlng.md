# Lab Title: Provisioning a VM under an Azure Virtual Network with All Components

## Lab Overview

In this lab, you will deploy and configure a secure environment in Azure by provisioning Virtual Machines within a Virtual Network (VNet) that contains both public and private subnets. You will test access scenarios to ensure proper network security.

---

## Pre-requisites

- An active Azure subscription  
- Basic knowledge of networking concepts  
- Familiarity with Virtual Machines (VMs) and SSH connections  

---

## Outcomes

By the end of this lab, you will:

1. Successfully create a VNet with public and private subnets.  
2. Deploy VMs in both subnets with appropriate network configurations.  
3. Implement and test network security rules.  
4. Validate secure and restricted access scenarios.  

---

## Description

This hands-on challenge focuses on provisioning and configuring Azure Virtual Machines within a secured Virtual Network. You will deploy two VMs, one in a public subnet and another in a private subnet, and configure Network Security Groups (NSGs) to enforce network isolation policies. You will test various access scenarios to validate security settings.

---

## Tasks

### Task 1: Build the Azure Virtual Network

**Goal:** Create a VNet with a public and private subnet.

#### Steps:

1. Navigate to the Azure Portal.  
2. Create a Virtual Network with the following settings:  
   - Address space: `10.0.0.0/16`  
   - Subnets:  
     - **PublicSubnet:** `10.0.1.0/24`  
     - **PrivateSubnet:** `10.0.2.0/24`  

📘 [Azure Virtual Network Quickstart Documentation](https://learn.microsoft.com/en-us/azure/virtual-network/quick-create-portal)

---

### Task 2: Deploy Virtual Machines

**Goal:** Launch two VMs in the public and private subnets, respectively.

#### Steps:

1. Deploy a Linux VM in `PublicSubnet`:  
   - Assign a public IP.  
   - Choose SSH for authentication.  
   - Deploy with the appropriate VM size and region settings.

2. Deploy a Linux VM in `PrivateSubnet`:  
   - Do not assign a public IP.  
   - Ensure the VM uses the appropriate network interface connected to `PrivateSubnet`.

📘 [Create a Linux Virtual Machine](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal)

---

### Task 3: Configure Security Rules

**Goal:** Implement NSG rules to control access.

#### Steps:

1. **Public Subnet NSG:**  
   - Allow inbound SSH traffic on port `22`.

2. **Private Subnet NSG:**  
   - Deny all inbound traffic from external sources.  
   - Allow traffic within the VNet.

3. Apply the NSGs to their respective subnets.

📘 [Network Security Groups Overview](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)

---

### Task 4: Test and Validate Connectivity

#### 1. Success Test: Public VM Access from Local Machine

**Steps:**

- SSH into the `PublicVM` using its public IP.  
- Ensure successful connection.

**Expected Outcome:**

- You should successfully connect to the Public VM.

#### 2. Success Test: Private VM Access from Public VM

**Steps:**

- SSH into `PrivateVM` from `PublicVM` using its private IP.  
- Ensure successful connection.

**Expected Outcome:**

- You should successfully connect to the Private VM.

#### 3. Failure Test: Direct Private VM Access from Local Machine

**Steps:**

- Attempt to SSH directly into `PrivateVM` from your local machine.  
- Ensure connection fails due to restricted access.

**Expected Outcome:**

- The connection should fail due to restricted access.

📘 [SSH into Azure Linux VM](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows)

---

## Submission Guidelines

- Provide screenshots of the following:  
  - Successful SSH connection to `PublicVM`.  
  - Successful SSH connection from `PublicVM` to `PrivateVM`.  
  - Failed direct connection attempt to `PrivateVM` from your local machine.  
- Provide a brief report summarizing your observations during the testing phase.  
- Submit all artifacts and documentation via the specified submission platform.

---

## Additional Resources

- [Azure Virtual Network Documentation](https://learn.microsoft.com/en-us/azure/virtual-network/)  
- [Manage NSG Rules](https://learn.microsoft.com/en-us/azure/virtual-network/manage-network-security-group)

