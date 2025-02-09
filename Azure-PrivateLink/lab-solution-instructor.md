# Configuring Azure Private Link for Azure Storage

## Notes to Instructor

### Key Points to Verify

- Ensure that the student has successfully created the Resource Group, Virtual Network (VNet), and subnets as instructed.
- Confirm the deployment of Azure Firewall with the correct configurations, including subnet assignment and public IP association.
- Verify the creation and application of both application and network rule collections.
- Ensure that the test scenarios for validating the firewall rules were executed correctly.
- Confirm that cleanup of all Azure resources was completed to avoid unnecessary charges.

### Common Challenges

- Students may face issues with assigning the correct subnet configurations for Azure Firewall.
- Application and network rule priorities or incorrect configurations might block expected traffic.
- Students may have trouble connecting to the test VM or verifying traffic control.
- Misconfigurations in the public IP or firewall policy setup could cause issues.

### Suggestions for Assistance

- Guide students in verifying subnet configurations and ensuring that `AzureFirewallSubnet` is correctly set up.
- Assist in troubleshooting rule configurations by reviewing priorities and settings.
- Ensure students have enabled public IP for the test VM and can connect via RDP or SSH.
- Recommend testing access to target and blocked sites thoroughly.
- Remind students to check firewall status in the portal to ensure it is running.

---


# Submission Checklist

- **Screenshot** showing the creation of the resource group.
- **Screenshot** of the virtual network and subnets configuration.
- **Screenshot** showing the Azure Firewall deployment with IP configurations.
- **Screenshot** of the application and network rule collections.
- **Screenshot** of successful and failed traffic tests.
- **Confirmation** of resource group deletion.
- **A brief report** summarizing the configurations and validations performed.

### Sample Report Summary

- **Resource Group Creation:** Successfully created a resource group named `AzureFirewallLabRG`.
- **Virtual Network Creation:** Created a virtual network `AzureFirewallVNet` with two subnets: `AzureFirewallSubnet` and `BackendSubnet`.
- **Azure Firewall Deployment:** Deployed `MyAzureFirewall` in `AzureFirewallSubnet` with a public IP address named `MyFirewallPublicIP`.

- **Rule Configuration:**
    - Application Rule Collection `AppRuleCollection1`: Allowed traffic to `www.microsoft.com`.
    - Network Rule Collection `NetRuleCollection1`: Allowed TCP traffic on ports 80 and 443 from `10.0.2.0/24`.

- **Testing:**
    - Successfully accessed `www.microsoft.com` from `TestVM`.
    - Confirmed access was denied to `www.blockedexample.com`.

- **Cleanup:** Deleted the resource group `AzureFirewallLabRG` and all associated resources.

### Troubleshooting and Additional Notes

- **Firewall Status:** Ensure the firewall status is Running before testing rules.
- **Connection Issues:** Verify NSG rules and ensure public IP is correctly configured for the test VM.
- **Testing Access:** Use browser and command-line tools for thorough validation.
- **Rule Priority:** Check for conflicting rule priorities if traffic behaves unexpectedly.

---

## Additional Resources

- [Azure Firewall Documentation](https://docs.microsoft.com/en-us/azure/firewall/)
- [Azure Networking Concepts](https://docs.microsoft.com/en-us/azure/virtual-network/)
- [Troubleshoot Azure Firewall](https://docs.microsoft.com/en-us/azure/firewall/troubleshoot)
- [Azure CLI Networking Commands](https://docs.microsoft.com/en-us/cli/azure/network)