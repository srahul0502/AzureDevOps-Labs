# Provisioning Azure DNS

## Notes to Instructor

### Key Points to Verify

- Ensure that the student has successfully created a DNS Zone in Azure.
- Confirm the creation and correct configuration of DNS records (A, CNAME, TXT).
- Verify that domain name resolution tests return expected results.
- Check that the cleanup process was completed to avoid unnecessary charges.

### Common Challenges

- Students may overlook specifying the correct DNS record types and values.
- TTL settings may be misconfigured, leading to unexpected caching behavior.
- Domain name resolution issues may arise due to incorrect record configurations.

### Suggestions for Assistance

- Guide students on how to properly configure DNS records and verify their values.
- Assist in resolving domain resolution issues by checking record propagation and ensuring correct public IP assignment.
- Recommend using tools like nslookup and dig for detailed testing.

---

## Submission Checklist

- Screenshot showing the DNS records created (A, CNAME, etc.).
- Screenshot of successful nslookup command outputs.
- A brief report summarizing domain name resolution verification steps and observations.

### Sample Report Summary

- **DNS Zone Creation:** Successfully created a DNS Zone for example.com.
- **DNS Record Configuration:** Added A record pointing to public IP and CNAME record for subdomain.
- **Domain Name Resolution Tests:** Verified successful resolution of both root domain and subdomain using nslookup.
- **Cleanup:** Deleted the DNS Zone and associated resources to avoid unnecessary charges.

By completing this lab, students gain practical experience in managing DNS zones and records in Azure, enhancing their understanding of DNS operations and resource management in cloud environments.
