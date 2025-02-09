# Configuring and Testing Azure NAT Gateway

## Notes to Instructor

### Verification Tips

- Ensure that the VNet and subnet are correctly created and configured for outbound traffic.
- Verify that the NAT Gateway is properly associated with the subnet and has the correct public IP address configured.
- Ensure that the VM is deployed in the correct subnet without a public IP address.
- Confirm that the NAT Gateway is properly routing outbound traffic from the VM by testing internet connectivity.
- Check that the correct route table is associated with the subnet, allowing the NAT Gateway to manage outbound internet traffic.
- Ensure that the VM can successfully access external websites (for example, using ping or curl commands).
- Monitor the NAT Gateway’s metrics to confirm proper functionality.

### Areas for Assistance

- Guide students on configuring the NAT Gateway and associating it with the subnet.
- Provide help in troubleshooting issues related to VM connectivity or routing, such as ensuring proper routing rules in the route table.
- Assist with the process of verifying that the VM does not have a public IP but still has internet access through the NAT Gateway.
- Help students with troubleshooting connectivity issues when verifying outbound traffic (e.g., check for firewall settings or incorrect network configurations).
- Provide insights on using Azure Network Watcher to monitor VM connectivity through the NAT Gateway.

### Common Challenges

- **VM Connectivity Issues:** Students may face issues where the VM cannot access external resources despite the NAT Gateway being configured correctly. This can occur if the route table is not correctly associated with the subnet or the NAT Gateway is not properly linked to the public IP.
- **Firewall Rules:** Ensure that firewall settings, both at the VM and network level, do not block outbound traffic. It may be necessary to allow specific ports or protocols for connectivity.
- **Public IP Configuration:** Sometimes, a public IP may mistakenly be assigned to the VM itself, bypassing the NAT Gateway. Ensure that the VM does not have a direct public IP assignment.
- **Incorrect Route Table Settings:** Ensure that the route table is set up correctly and is associated with the subnet for proper outbound traffic routing.
- **Scaling Issues with NAT Gateway:** As workloads increase, there might be challenges related to the scalability of the NAT Gateway. Ensure students understand how to monitor NAT Gateway usage and scale if needed.

### Suggestions for Assistance

- Provide clear explanations for troubleshooting outbound connectivity, including checking for route table misconfigurations.
- If students are facing issues with the VM not accessing external websites, guide them to check Network Watcher and routing details to ensure proper path configurations.
- For scaling issues or heavy traffic, suggest monitoring the NAT Gateway's metrics and considering additional configurations or different setup options if necessary.

---

## Submission Checklist

- **Screenshot** of the VNet and Subnet creation.
- **Screenshot** of the NAT Gateway configuration and the public IP association.
- **Screenshot** of the NAT Gateway's association with the subnet.
- **Screenshot** of the VM creation and the network configuration (ensure no public IP is assigned).
- **Screenshot** showing the outbound connectivity test results from the VM (e.g., using ping or curl commands).
- **Screenshot** of the NAT Gateway’s metrics and monitoring output.

### Sample Report Summary

- **Verification Tips:**
    - Verified that the NAT Gateway was correctly configured and associated with the subnet.
    - Ensured that the VM was able to access external resources via outbound traffic without a public IP.
    - Checked the correct routing paths in the route table associated with the subnet.

- **Areas for Assistance:**
    - Students may need assistance configuring the NAT Gateway and associating it with the subnet.
    - Troubleshooting outbound connectivity might require additional support with route tables and VM firewall settings.
    - Scaling the NAT Gateway might require monitoring and adjustments, especially if the workload increases.

---

## Additional Notes

- Remind students that NAT Gateway ensures outbound internet connectivity for VMs without requiring a public IP address on the VM itself.
- Encourage students to use Network Watcher for more in-depth troubleshooting and to monitor the traffic paths of their VM through the NAT Gateway.
- Provide guidance on scaling the NAT Gateway for large-scale deployments or high-traffic applications.
