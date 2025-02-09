# Provisioning an Azure Monitor Alert for VM Deletion Events

## Notes to Instructor

### Common Challenges and Tips

1. **Activity Log Filtering Issues:**  
   - Students might overlook filtering by the correct operation type.  
   - **Tip:** Ensure students filter for `Microsoft.Compute/virtualMachines/delete` under the **Administrative** category.

2. **Log Analytics Workspace Integration:**  
   - Students may forget to link the Activity Logs to the workspace.  
   - **Tip:** Verify the integration by confirming the appearance of recent logs in the workspace.

3. **Alert Rule Configuration Issues:**  
   - Students might misconfigure the KQL query or threshold in the alert.  
   - **Tip:** Emphasize testing the query in Log Analytics before using it in the alert rule.

4. **Notification Failures:**  
   - Students may forget to configure or validate action groups for notifications.  
   - **Tip:** Test the notification method (e.g., email) separately to ensure delivery.

---

## Submission Checklist

- **Screenshots of:**  
  - Activity Log filtered for VM deletion events  
  - Log Analytics workspace showing linked Activity Logs  
  - Alert rule configuration  
  - Notification of the triggered alert  
- A brief report summarizing:  
  - Challenges faced and solutions applied  
  - Steps to verify the alert

---

## Solution

### **Step 1: Analyze VM Deletion Logs**

1. Open **Azure Portal** and navigate to **Monitor > Activity Log**.  
2. Set filters:  
   - **Category:** Administrative  
   - **Operation Type:** Delete  
3. Search for events with the resource type `Microsoft.Compute/virtualMachines/delete`.

💡 **Instructor Tip:** Explain the importance of Activity Logs in tracking administrative actions.

---

### **Step 2: Configure a Log Analytics Workspace**

1. Go to **Azure Monitor > Log Analytics workspaces**.  
2. Click **Create** and configure the workspace:  
   - **Name:** VMDeletionLogs  
   - **Region:** Same as the subscription resources  
3. Navigate to **Activity Logs > Diagnostic settings**, and add a diagnostic setting:  
   - Select **Send to Log Analytics workspace**.  
   - Choose the created workspace.  
   - Enable **Administrative operations**.

💡 **Instructor Tip:** Highlight how linking Activity Logs enables querying logs using KQL.

---

### **Step 3: Create an Alert Rule**

1. Go to **Azure Monitor > Alerts** and click **Create Alert Rule**.  
2. Configure the alert source:  
   - Select **Log Analytics** as the data source.  
   - Choose the workspace created earlier.  
3. Write the query to detect VM deletion events:

   ```kql
   AzureActivity  
   | where OperationNameValue == "Microsoft.Compute/virtualMachines/delete"  
   | where ActivityStatusValue == "Succeeded"  
   ```

4. Set up the alert condition:  
   - **Threshold:** Greater than 0 results  
   - **Evaluation period:** 5 minutes  
5. Create an action group for notifications:  
   - **Name:** VMDeletionAlertGroup  
   - Add actions (e.g., email, SMS).  
6. Review and activate the alert.

💡 **Instructor Tip:** Guide students on using evaluation periods to minimize false positives.

---

### **Step 4: Test the Alert**

1. Deploy a test VM:  
   - Navigate to **Virtual Machines** and create a VM.  
   - Use default settings for simplicity.  
2. Delete the VM:  
   - Go to the VM resource page and click **Delete**.  
3. Monitor the alert:  
   - Confirm that the alert triggers and the notification is received.

💡 **Instructor Tip:** Encourage students to use different scenarios (e.g., multiple VMs) to test the alert’s reliability.

---

## Sample Report Summary

**Challenges and Solutions:**  
- **Issue:** Misconfigured KQL query in the alert.  
  - **Solution:** Tested the query in Log Analytics and corrected syntax errors.  
- **Issue:** Notification not received.  
  - **Solution:** Verified action group settings and tested email delivery separately.

**Verification Steps:**  
- Checked the Activity Log for `Microsoft.Compute/virtualMachines/delete` events.  
- Verified alert activation and notification delivery after deleting a test VM.

**Common Errors:**  
- Forgetting to link Activity Logs to the Log Analytics workspace.  
- Incorrectly setting the alert rule condition or evaluation period.

---

## Additional Notes

- Encourage students to explore additional Azure Monitor features, such as custom queries and dashboards.  
- Highlight the significance of alerts in maintaining resource compliance and security.
