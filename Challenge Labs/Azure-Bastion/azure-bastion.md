# Lab Title: Provision Azure Bastion to Connect to Virtual Machines (SSH & RDP)

## Lab Overview

In this lab, you will learn how to set up Azure Bastion, a service that provides secure and easy access to your virtual machines (VMs) in Azure. With Azure Bastion, you can connect to your VMs securely using either SSH for Linux machines or RDP for Windows machines, without the need for a public IP address.

## Pre-requisites

- An active Azure account.
- A virtual network (VNet) set up in Azure.
- At least one virtual machine already created in Azure (either Linux or Windows).
- Basic understanding of how virtual machines work in Azure.

## Learning Objectives

By the end of this lab, you will:

- Understand what Azure Bastion is and how it helps keep your virtual machines secure.
- Learn how to set up Azure Bastion in your virtual network.
- Be able to connect to virtual machines securely using Azure Bastion (both SSH for Linux and RDP for Windows).

## Lab Description

This lab will guide you step-by-step in setting up Azure Bastion, and connecting to your virtual machines in Azure securely. You won’t need a public IP to access your VMs—Bastion does that for you, keeping your connections secure.

## TASKS

### Task 1: Set Up Azure Bastion

**Objective:** Set up Azure Bastion to securely connect to virtual machines in your network.

**Instructions:**

1. Go to the Azure Portal.
2. In the search bar at the top, type Bastion and select Bastions from the results.
3. Click on Create to start the process of creating Azure Bastion.
4. Fill out the information for your Bastion setup:
    - **Subscription:** Choose your subscription (usually the default one).
    - **Resource Group:** Either select an existing group or create a new one. A resource group is like a folder that holds related resources.
    - **Name:** Give your Bastion a unique name (e.g., SecureBastion).
    - **Region:** Choose the region where your resources are located.
    - **Virtual Network:** Select the virtual network (VNet) where your virtual machines are located. If you don’t have a VNet, you’ll need to create one.
    - **Subnet:** Azure will automatically create a bastion subnet for you. This is where the Bastion service will live.
    - **Public IP Address:** Create a new public IP for Bastion to use. This helps make sure you can securely access your machines.
5. Click Review + Create to check your settings, then click Create to set up Bastion.

### Task 2: Connect to a Virtual Machine Using Azure Bastion

**Objective:** Use Azure Bastion to securely connect to a virtual machine (VM).

**Instructions:**

1. In the Azure Portal, go to the Virtual Machines section and select the VM you want to connect to.
2. In the VM page, click Connect and then select Bastion.
3. Azure will show a connection window with options to connect using SSH for Linux VMs or RDP for Windows VMs.
4. Enter your login details:
    - **For SSH (Linux VM):** Provide the username and either the private key or password you set when the VM was created.
    - **For RDP (Windows VM):** Enter the username and password you created for your Windows VM.
5. Click Connect to establish a secure connection to the VM.

### Task 3: Test the Connection

**Objective:** Ensure that you can connect to the VM successfully using Azure Bastion.

**Instructions:**

1. For Linux VMs: When you use SSH, a terminal window will open, and you should be able to run commands directly on the VM.
2. For Windows VMs: If you're using RDP, the Windows desktop of your VM will appear.
3. Confirm that you can interact with your VM and verify the connection is working.

### Task 4: Clean Up (Optional)

**Objective:** Remove resources after testing to avoid unnecessary charges.

**Instructions:**

1. Go to the Resource Group where your Bastion setup and virtual machine are stored.
2. Select the Bastion host and click Delete.
3. Confirm the deletion by entering the resource name as prompted.
4. Optionally, delete the associated public IP and bastion subnet if not required.

## Submission Guidelines

- Take a screenshot showing the successful connection to your virtual machine using Azure Bastion.
- Include a brief explanation of the connection method you used (SSH or RDP).
- Submit the screenshot and explanation through the designated submission portal.

## Additional Resources

- [Azure Bastion Overview](https://learn.microsoft.com/en-us/azure/bastion/bastion-overview/)
- [How to Use Azure Bastion](https://learn.microsoft.com/en-us/azure/bastion/bastion-connect-vm/)
