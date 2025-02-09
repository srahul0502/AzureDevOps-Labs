# Provisioning a VM under an Azure Virtual Network with All Components

## Notes to Instructor

### Key Points to Verify

- Ensure that the student has successfully created a Virtual Network (VNet) with both public and private subnets.
- Confirm proper deployment of two Virtual Machines (VMs): one in the public subnet and the other in the private subnet.
- Verify the configuration of Network Security Groups (NSGs) and their corresponding rules.
- Check that connectivity tests have been performed correctly, including successful and failed SSH attempts.

### Common Challenges

- Students may overlook assigning the correct subnet during VM deployment.
- NSG rules may not be applied correctly, leading to unintended access.
- Connectivity issues could arise if the private subnet VM lacks a route through the public subnet VM.

### Suggestions for Assistance

- Guide students on verifying NSG configurations and effective rule priority.
- Assist in debugging SSH connectivity issues by checking IP configurations and routing settings.
- Recommend the use of Azure Cloud Shell for easier SSH access.

---

## Solution

### Task 1: Build the Azure Virtual Network

**Steps to Solution:**

1. Navigate to the Azure Portal.
2. Select Create a resource and choose Virtual Network.
3. Configure the following settings:
    - **Name:** LabVNet
    - **Address space:** 10.0.0.0/16
    - **Subnets:**
        - **PublicSubnet:** 10.0.1.0/24
        - **PrivateSubnet:** 10.0.2.0/24
4. Review and create the VNet.

### Task 2: Deploy Virtual Machines

**Steps to Solution:**

**Deploy the Public VM:**

1. Navigate to the Azure Portal and select Create a resource.
2. Choose Virtual Machine.
3. Configure the following:
    - **Name:** PublicVM
    - **Region:** Same as the VNet
    - **Subnet:** PublicSubnet
    - **Public IP:** Enabled
    - **Authentication type:** SSH (use an existing or generate a new key pair)
4. Review and create the VM.

**Deploy the Private VM:**

1. Repeat the above steps but configure the following:
    - **Name:** PrivateVM
    - **Subnet:** PrivateSubnet
    - **Public IP:** Disabled
2. Review and create the VM.

### Task 3: Configure Security Rules

**Steps to Solution:**

**Public Subnet NSG:**

1. Navigate to the NSG associated with PublicSubnet.
2. Add an inbound rule:
    - **Source:** Any
    - **Protocol:** TCP
    - **Port range:** 22
    - **Action:** Allow

**Private Subnet NSG:**

1. Navigate to the NSG associated with PrivateSubnet.
2. Add an inbound rule:
    - **Source:** Virtual Network
    - **Protocol:** Any
    - **Action:** Allow
3. Ensure the default rule denying all other traffic is present.

### Task 4: Test and Validate Connectivity

1. **Success Test: Public VM Access from Local Machine**

    **Steps:**

    - Open a terminal and run:
        
        ```ssh azureuser@<PublicVM_Public_IP>```
        
    - Ensure successful SSH connection.

2. **Success Test: Private VM Access from Public VM**

    **Steps:**

    - From the PublicVM, run:
        
        ```ssh azureuser@<PrivateVM_Private_IP>```
        
    - Ensure successful SSH connection.

3. **Failure Test: Direct Private VM Access from Local Machine**

    **Steps:**

    - Attempt to SSH directly to PrivateVM:
        
        ```ssh azureuser@<PrivateVM_Private_IP>```
        
    - Verify that the connection fails due to restricted access.

---

## Submission Checklist

- Screenshot of successful SSH connection to PublicVM.
- Screenshot of successful SSH connection from PublicVM to PrivateVM.
- Screenshot showing the failed SSH attempt directly to PrivateVM.
- A brief report summarizing observations during testing.

### Sample Report Summary

- **VNet Configuration:** Successfully created a VNet with public and private subnets.
- **VM Deployment:** Deployed VMs in the correct subnets.
- **NSG Rules:** Configured rules to allow secure access.
- **Connectivity Tests:** Verified successful and failed access scenarios as expected.

By completing this lab, students gain hands-on experience with Azure networking and security concepts, enhancing their understanding of cloud resource management.
