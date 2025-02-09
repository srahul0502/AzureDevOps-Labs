# **Lab Title:** Provision an Azure Monitor Alert for VM Deletion Events  

## **Lab Overview**  
In this challenge lab, you will configure Azure Monitor to detect and alert when a virtual machine (VM) deletion occurs in your subscription. You will be required to analyze logs, set up alerts, and test notifications independently.  

## **Pre-requisites**  
- An active **Azure subscription**  
- Familiarity with Azure Monitor and Log Analytics  
- Understanding of Azure Resource Manager (ARM)  
- Permissions to create resources and access logs  

## **Learning Objective**  
By the end of this lab, participants will:  
- Create and configure an alert rule in Azure Monitor  
- Use Log Analytics to track resource deletion events  
- Test and verify alert notifications  

## **Description**  
Azure Monitor provides a powerful solution for monitoring Azure resources. In this lab, your task is to set up an alert that triggers whenever a virtual machine deletion occurs within your subscription. This requires querying Activity Logs and configuring alert rules without guided steps.  

---

## **Tasks**  

### **Task 1: Analyze VM Deletion Logs**  
**Objective:** Identify log entries that capture VM deletions.  

**Instruction:**  
1. Open the **Azure Portal** and navigate to **Activity Log** under **Monitor**.  
2. Filter logs by the category **Administrative** and the operation type **Delete**.  
3. Analyze the event properties for VM deletion events.  

**Verification:**  
- Confirm that you have found events with `Microsoft.Compute/virtualMachines/delete` in the logs.  

---

### **Task 2: Configure a Log Analytics Workspace**  
**Objective:** Set up a Log Analytics workspace for querying Activity Logs.  

**Instruction:**  
1. Navigate to **Azure Monitor > Log Analytics workspaces**.  
2. Create a new Log Analytics workspace if none exists.  
3. Link the **Activity Logs** of your subscription to this workspace.  

**Verification:**  
- Ensure successful integration by viewing recent log entries in the workspace.  

---

### **Task 3: Create an Alert Rule**  
**Objective:** Configure an alert for VM deletion events.  

**Instruction:**  
1. Go to **Azure Monitor > Alerts** and select **Create Alert Rule**.  
2. Choose your Log Analytics workspace as the data source.  
3. Write a query to detect VM deletion events from logs.  
4. Configure the alert condition, threshold, and action group for notifications.  

**Verification:**  
- Ensure the alert is successfully created and active.  

---

### **Task 4: Test the Alert**  
**Objective:** Verify the alert by deleting a test VM.  

**Instruction:**  
1. Deploy a test virtual machine.  
2. Delete the virtual machine.  
3. Monitor the alert notifications.  

**Verification:**  
- Confirm the alert was triggered and notification was received.  

---

## **Submission Guidelines**  
- Submit the following evidence:  
  - Screenshots of the alert rule configuration  
  - Log query results showing VM deletion events  
  - Screenshot of the received notification  
- Include a brief report on challenges faced and solutions.  

---

## **Additional Resources**  
- [Azure Monitor Documentation](https://learn.microsoft.com/en-us/azure/azure-monitor/)  
- [Kusto Query Language (KQL) Reference](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/)  
- [Activity Logs in Azure](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/activity-log)  
