# Virtual Machine Extension with Custom Script in Azure

## Notes to Instructor

### Common Challenges and Tips

**Custom Script Extension Installation Issues:**
- Users may encounter errors when installing the Custom Script Extension.
- **Tip:** Ensure the correct extension is selected for the operating system (e.g., Linux or Windows).

**Script Execution Failures:**
- Scripts may not run due to incorrect paths or syntax errors.
- **Tip:** Verify the script’s permissions, path, and content before deployment.

**Troubleshooting Logs:**
- Students may overlook the logs for debugging script execution failures.
- **Tip:** Emphasize checking the extension status and logs in "Extensions + applications" to identify issues.

**Verification Challenges:**
- Users may face difficulty confirming script success.
- **Tip:** Provide examples of verification commands or steps.

## Submission Checklist

- **Screenshots:**
  - Custom Script Extension installed and execution status
  - Logs showing successful script execution
  - Command output or evidence confirming successful script execution
- Brief explanation of the script’s purpose and encountered challenges

## Solution

### Step 1: Install the Custom Script Extension on a Virtual Machine

**Navigate to the Azure Portal:**
- Open [Azure Portal](https://portal.azure.com) and log in with your credentials.

**Select or Create a Virtual Machine:**
1. Go to **Virtual Machines** and select an existing VM or create a new one.
2. Ensure the VM has a public IP or appropriate access for remote management.

**Install the Custom Script Extension:**
1. Navigate to **Extensions + applications** under the selected VM.
2. Click **+ Add**, search for **Custom Script Extension**, and select it.
3. Upload the custom script file or provide a URL to the script.
4. Click **OK** to install and configure the extension.

**Verification:**
- Confirm that the extension appears under "Extensions + applications" with the status **Provisioning succeeded**.

💡 **Instructor Tip:** Highlight the importance of using secure URLs and verifying script file integrity.

### Step 2: Execute the Custom Script on the Virtual Machine

**Monitor Script Execution:**
- Check the extension status in the Azure Portal.
- Navigate to the VM’s "Extensions + applications" section and select the Custom Script Extension.
- View the status and logs to confirm execution.

**Verification:**
- Validate that the script ran successfully and check for any error messages.
- Review logs for details on script execution.

💡 **Instructor Tip:** Encourage students to use `tail` (Linux) or Event Viewer (Windows) for deeper log inspection.

### Step 3: Verify the Custom Script Execution

**Log in to the VM:**
- Use SSH for Linux VMs or RDP for Windows VMs.

**Check Script Outcomes:**
1. Verify the expected changes (e.g., software installation, file updates).
2. Run appropriate verification commands.
   - Example for Linux: `sudo systemctl status <service-name>`
   - Example for Windows: Check the installed programs list or configuration files.

**Verification:**
- Provide evidence such as command outputs or screenshots confirming the script’s success.

💡 **Instructor Tip:** Provide common verification commands relevant to typical tasks.

### Step 4: Troubleshoot Script Execution (If Necessary)

**Identify Issues:**
- Check failure logs in "Extensions + applications."
- Review the script for syntax errors or missing dependencies.

**Modify and Re-run Script:**
1. Update the script as needed.
2. Re-upload and execute the updated script.

**Verification:**
- Ensure the script runs without errors and that intended changes are applied.
- Confirm the extension status is **Provisioning succeeded**.

💡 **Instructor Tip:** Encourage students to document troubleshooting steps and resolutions.

## Sample Report Summary

**Verification Tips:**
- **Extension Installation:** Confirm "Provisioning succeeded" status.
- **Script Execution:** Check logs for success indicators.
- **Outcome Validation:** Provide evidence of successful execution.

**Common Errors:**
- Incorrect script paths or permissions
- Missing dependencies
- Network connectivity issues

**Troubleshooting Tips:**
- Use logs to identify and resolve issues.
- Verify script syntax and test independently before deployment.

## Additional Notes

- Encourage independent problem-solving and critical thinking.
- Highlight best practices for secure and efficient automation using Custom Script Extensions in Azure.

