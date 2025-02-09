# Lab Title

Deploying and Configuring a High-Availability Azure Load Balancer

## Lab Overview

This lab challenges you to provision and configure a public-facing Azure Load Balancer. You'll independently deploy the necessary infrastructure and validate traffic distribution across multiple backend services, ensuring a scalable and highly available architecture.

## Pre-requisites

- Active Azure subscription
- Familiarity with:
    - Virtual Networks, Virtual Machines (VMs), and Load Balancers
    - Network security configurations
- Experience with Azure CLI, PowerShell, or Azure Portal

## Learning Objectives

By completing this lab, you will:

- Deploy and configure network and compute infrastructure
- Set up and monitor an Azure Load Balancer
- Implement backend pools, health probes, and load balancing rules
- Validate proper traffic distribution and service availability


## Description

You are tasked with creating a load-balanced environment in Azure for handling web traffic. Configure the Load Balancer to distribute incoming HTTP requests to multiple backend VMs while monitoring their health and ensuring traffic is evenly balanced.

# Tasks

## Task 1: Deploy Network Infrastructure

**Objective:** Set up a secure and scalable virtual network

**Instructions:**

- Create a virtual network (VNet) with an address space of 10.0.0.0/16
- Define a subnet with the address range 10.0.1.0/24 within the VNet
- Ensure appropriate Network Security Groups (NSGs) allow inbound traffic on port 80

**Verification:**
- Confirm the VNet and subnet are created correctly and visible in the Azure Portal

## Task 2: Deploy Backend Virtual Machines (VMs)

**Objective:** Create virtual machines to form the backend pool

**Instructions:**

- Deploy at least two Linux or Windows VMs within the subnet created
- Ensure that each VM has a web server running (such as NGINX or IIS) to respond to HTTP requests
- Open port 80 on each VM

**Verification:**
- Verify that HTTP traffic reaches each backend VM independently

## Task 3: Create the Load Balancer

**Objective:** Set up a public-facing load balancer to manage traffic

**Instructions:**

- Create a public IP address for the load balancer
- Configure the frontend IP for the load balancer
- Create a backend pool and add the VMs to it

**Verification:**
- Confirm the public IP is assigned to the load balancer

## Task 4: Configure Health Probes

**Objective:** Monitor the health of backend resources

**Instructions:**

- Set up a health probe on port 80
- Ensure the health probe monitors VM availability

**Verification:**
- Validate that all backend VMs are healthy as per the health probe configuration

## Task 5: Create Load Balancing Rules

**Objective:** Distribute HTTP traffic across backend resources

**Instructions:**

- Define a load balancing rule for port 80
- Map frontend traffic to backend VMs

**Verification:**
- Confirm the rule is applied correctly and visible in the configuration

## Task 6: Test Traffic Distribution

**Objective:** Verify proper traffic distribution across backend VMs

**Instructions:**

- Access the load balancer's public IP from a web browser
- Observe responses from different backend VMs as traffic is distributed

**Verification:**
- Demonstrate that multiple backend VMs are serving traffic

---

## Submission Guidelines

Submit the following:

- **Architecture Diagram:** Visualize the network and load balancer configuration
- **Screenshots:**
    - Virtual network and subnet configuration
    - Load balancer settings with backend pools, health probes, and rules
    - Test results validating traffic distribution
- **Verification Report:** Brief explanation of steps taken and results observed

## Additional Resources

- [Azure Load Balancer Documentation](https://docs.microsoft.com/en-us/azure/load-balancer/)
- [Microsoft Learn: Configure a Load Balancer](https://docs.microsoft.com/en-us/learn/modules/configure-azure-load-balancer/)
