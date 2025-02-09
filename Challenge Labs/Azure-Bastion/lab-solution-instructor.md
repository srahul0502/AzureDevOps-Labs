# Provisioning Azure Bastion to Connect to Virtual Machines (SSH & RDP)

## Notes to Instructor

### Key Points to Verify

- Ensure that the student has successfully created an Azure Bastion resource.
- Verify that Azure Bastion is configured to connect to the virtual machines within the correct virtual network (VNet).
- Confirm that the student can connect to both Linux (SSH) and Windows (RDP) virtual machines using Azure Bastion.
- Check that the cleanup process was completed to avoid unnecessary charges.

### Common Challenges

- Students may overlook correctly configuring the Bastion subnet, which can prevent successful connections.
- Incorrect VM login credentials (SSH key or RDP password) may cause connection issues.
- The public IP address for Bastion may not be configured correctly, leading to inaccessible services.

### Suggestions for Assistance

- Guide students on ensuring the Bastion subnet is properly configured and part of the virtual network.
- Provide assistance in verifying SSH key or RDP login credentials for correct access to virtual machines.
- Help students confirm that the necessary public IP for Azure Bastion is set up correctly, and assist with troubleshooting connection failures.

---

## Submission Checklist

- Screenshot showing the successful connection to a virtual machine via Azure Bastion (SSH for Linux or RDP for Windows).
- A brief explanation of the connection method used (SSH or RDP), including the login credentials used for each.
- A report summarizing the steps taken to configure Azure Bastion, successfully connect to a VM, and any troubleshooting steps followed.

### Sample Report Summary

- **Bastion Setup:** Successfully set up Azure Bastion in a new Resource Group with a public IP, and configured the Bastion subnet within the VNet.
- **Connection to VM:** Connected to both a Linux VM via SSH and a Windows VM via RDP, confirming secure access through Azure Bastion.
- **Connection Method:** Used SSH with private key for Linux VM, and RDP with password for Windows VM.
- **Cleanup:** Deleted Azure Bastion resource, public IP, and VM subnet after testing to avoid unnecessary charges.

By completing this lab, students will gain hands-on experience in securely managing connections to virtual machines in Azure using Azure Bastion, reinforcing their skills in cloud security and resource management.
