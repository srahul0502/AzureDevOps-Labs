# Azure Route Server and BGP Configuration Lab - Solution

## Notes to Instructor

### Key Points to Verify

- Ensure that the student has successfully created a Resource Group, Virtual Network (VNet), and subnets.
- Verify the deployment of the Azure Route Server and the creation of BGP peering with the VMs.
- Confirm that the VMs can communicate successfully both before and after configuring BGP.
- Ensure that the dynamic routing is correctly propagated and visible in the routing tables of the VMs.
- Verify that BGP is properly configured and that the routes are being advertised and learned by the Azure Route Server and VMs.
- Confirm that the traceroute and routing table commands are used effectively to verify the dynamic route propagation.

### Common Challenges

- Students may struggle with configuring BGP peering or misconfigure ASN values.
- If connectivity issues persist, there may be incorrect subnet or NSG (Network Security Group) configurations.
- The BGP peering might not establish if the IP addresses or ASN values are incorrectly set.
- The routing table might not show dynamic routes if the BGP session is not established or configured properly.

### Suggestions for Assistance

- Guide the student through checking the BGP status in the Azure portal and ensure that the peering is correctly established.
- Assist in troubleshooting connectivity issues by verifying subnet configurations and NSG rules.
- Recommend using network troubleshooting tools like `ping`, `traceroute`, and `ip route show` to ensure proper routing.
- Verify that the correct private IP addresses are used in the peering configuration.

---

## Submission Checklist

- Screenshot showing the Azure Route Server and BGP peering configuration.
- Screenshot of the routing table on TestVM1, displaying dynamically learned routes.
- Screenshot of traceroute output from TestVM1 to TestVM2.
- A brief report summarizing the BGP configuration, dynamic routing verification, and troubleshooting steps.

### Sample Report Summary

- **Resource Group Creation:** Successfully created a Resource Group named `SimpleRouteServerLab`.
- **Virtual Network Creation:** Created a Virtual Network `SimpleLabVNet` with two subnets: `TestSubnet` and `RouteServerSubnet`.
- **Azure Route Server Deployment:** Deployed `SimpleRouteServer` in the same VNet and subnet.
- **VM Deployment:** Deployed two VMs (`TestVM1` and `TestVM2`) in the `TestSubnet` and verified basic connectivity between them.
- **BGP Peering Configuration:** Configured BGP peering between `SimpleRouteServer` and `TestVM1` with ASN `65001`.
- **Dynamic Routing Verification:** The routing table on `TestVM1` displayed dynamic routes propagated by BGP, and `ping` tests were successful between VMs.
- **Traceroute:** The traceroute showed that traffic passed through the Azure Route Server, confirming proper BGP configuration.
- **Cleanup:** Deleted the Resource Group and associated resources to avoid unnecessary charges.

By completing this lab, students gain hands-on experience in configuring dynamic routing using Azure Route Server and BGP, enhancing their understanding of routing protocols in cloud environments.
