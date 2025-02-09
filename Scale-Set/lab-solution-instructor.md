# Configuring a Virtual Machine Scale Set in Azure

## Notes to Instructor

This lab provides hands-on experience with setting up a Virtual Machine Scale Set (VMSS) in Azure. It covers creating a scale set, configuring scaling rules, and verifying the deployment. Ensure that participants understand the key concepts of VM scaling and high availability.

### Common Challenges

- **Resource Limit Errors:** Participants may encounter subscription or quota limitations when creating multiple VM instances.  
  **Suggestion:** Guide them to check their Azure subscription quotas and reduce the VM size if needed.

- **SSH Key Issues:** Users may face issues with SSH key configurations during VM deployment.  
  **Suggestion:** Encourage participants to generate keys using tools like `ssh-keygen` and validate the public key format.

- **Scaling Configuration Errors:** Participants might misconfigure automatic scaling rules.  
  **Suggestion:** Emphasize the importance of setting meaningful CPU thresholds (e.g., scaling out at 70% CPU utilization).

---

### Submission Checklist

- Screenshot of the Virtual Machine Scale Set showing the number of VM instances running and their configurations.  
- Brief explanation of how scaling works in VMSS.  
- Description of any challenges faced and their solutions.

---

### Sample Report Summary

**Verification Tips:**  
- Ensure the scale set has the specified number of VM instances running.  
- Confirm that the instances are in a healthy state and the scaling configurations are correctly applied.  

**Areas for Assistance:**  
- Verify scaling rule configurations and thresholds if scaling is not functioning as expected.  
- Assist with resolving quota limitations by guiding students to use smaller VM sizes.  
- Help troubleshoot SSH key issues by validating key formats and usage.

---

### Solution:

1. Navigate to the [Azure Portal](https://portal.azure.com).  
2. Create a Virtual Machine Scale Set with the following parameters:  
   - **Region:** Preferred Azure region  
   - **VM Image:** Ubuntu Server 20.04 LTS  
   - **VM Size:** Standard B1s  
   - **Scaling Rule:** Scale out to 3 instances if CPU utilization exceeds 70%  
3. Deploy the VM Scale Set and validate the scaling configuration.  
4. Submit a screenshot of the successful deployment and instance details.

---

## Additional Notes

- Highlight the advantages of using VMSS for high availability and fault tolerance.  
- Encourage participants to explore setting up custom scaling rules beyond CPU-based metrics.  
- Provide resources on Azure Monitor to visualize scaling operations and instance health.
