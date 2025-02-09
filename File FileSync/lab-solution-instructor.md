 Hybrid File Synchronization using Azure Files and File Sync (Guided Lab)

## Notes to Instructor

This lab guides students through setting up Azure File Share and configuring Azure File Sync with an on-premises Windows Server. The goal is to provide practical experience in hybrid file synchronization, a common use case in enterprise environments.

### Common Challenges

#### Azure Resource Deployment Failures:
- Ensure students have the correct subscription and permissions to deploy resources.
- Remind them to select the same region for all related resources.

#### Server Registration Issues:
- Verify that the Azure File Sync agent is correctly installed and that the server is connected to the internet.
- Encourage students to check firewall settings and endpoint requirements.

#### Data Synchronization Errors:
- Ensure cloud tiering and sync policies are configured correctly.
- Guide students to check the Sync Group status and logs for error messages.

### Suggestions for Assistance
- Provide an overview of the lab objectives before starting.
- Walk students through Azure Portal navigation to avoid confusion.
- Encourage questions during server setup and sync configuration steps.
- Be ready to assist with RDP connection issues during the Windows Server setup.

## Submission Checklist
- Screenshot of the created Azure File Share.
- Screenshot of the Sync Group configuration.
- Screenshot showing the registered Windows Server.
- Evidence of successful file sync:
  - File created in the local folder appears in the Azure File Share.
  - File uploaded to Azure File Share appears in the local folder.

## Sample Report Summary
The student successfully completed the lab by provisioning an Azure File Share, configuring Azure File Sync, registering a Windows Server, and verifying bidirectional file synchronization.

### Verification Tips:
- Check that the Windows Server appears as a registered server in Azure File Sync.
- Confirm that the test files (`testfile.txt` and `syncverify.txt`) appear in both the local and cloud environments.

### Areas for Assistance:
- Troubleshoot registration failures by verifying the student's subscription access and the Azure File Sync agent installation.
- Assist in configuring the correct file path for server endpoints.
- Help with RDP connectivity issues during server setup.

### Solution
**Step 1:** Create the Azure File Share by navigating to the storage account and configuring a share with appropriate quota settings.

**Step 2:** Deploy Azure File Sync and create a sync group linked to the file share.

**Step 3:** Spin up a Windows Server VM in Azure, install the Azure File Sync agent, and register the server.

**Step 4:** Configure a server endpoint for sync, ensuring the path points to `C:\LabSyncFolder`. Create test files and verify synchronization.

**Step 5:** Validate bidirectional file sync by checking for file appearance in both the Azure File Share and the on-premises folder.

## Additional Notes
- Encourage students to document errors and solutions during the lab for troubleshooting practice.
- Highlight the importance of cloud tiering for managing storage costs.
- Suggest exploring additional features of Azure Files, such as role-based access control (RBAC) and backup integration.

