# Lab Title: Virtual Machine Extension - Custom Script in Azure

## Lab Overview

In this guided lab, you will learn how to use Azure Virtual Machine Extensions to run custom scripts on Virtual Machines (VMs). Virtual Machine Extensions are lightweight components that provide post-deployment configuration and automation on Azure VMs. By the end of this lab, you will have hands-on experience in deploying a custom script to automate tasks such as software installation or configuration on a VM.

## Pre-requisites

- An active Azure subscription with the necessary permissions to create resources.
- Basic understanding of Azure Virtual Machines and the Azure Portal.
- Familiarity with scripting (e.g., Bash, PowerShell) and automation tasks.

## Learning Objectives

By the end of this lab, you will be able to:

- Understand the role of Virtual Machine Extensions in Azure.
- Deploy and configure a custom script extension on a Virtual Machine.
- Automate post-deployment tasks such as installing packages or modifying configurations using a custom script.
- Verify and troubleshoot the execution of custom scripts on VMs.

## Lab Description

This lab walks you through the process of using the Custom Script Extension for Azure Virtual Machines. You will learn how to deploy and execute custom scripts for various automation tasks and gain insight into how VM extensions can streamline your post-deployment workflows.

## TASKS

### Task 1: Install Custom Script Extension on a Virtual Machine

**Objective:** Deploy the Custom Script Extension to a Virtual Machine in Azure.

**Instructions:**

1. Navigate to the Azure Portal.
2. In the search bar, type Virtual Machines and select the VM on which you want to run the custom script.
3. In the Overview tab of the VM, click on Extensions + applications under the Settings section.
4. Click Add and then select Custom Script for Linux (for Linux VMs) or Custom Script for Windows (for Windows VMs).
5. Upload your custom script file (e.g., a .sh file for Linux or .ps1 file for Windows) by clicking Browse for files and selecting the script.
6. Click OK to install the extension and apply the script.

### Task 2: Execute the Custom Script on the Virtual Machine

**Objective:** Run the uploaded custom script on the Virtual Machine.

**Instructions:**

1. Once the extension is installed, go to the Extensions + applications section again.
2. Verify that the Custom Script Extension is listed.
3. In the Status column, check if the script ran successfully or if there were any errors.
4. If the script did not run successfully, click on the extension name for more detailed logs and error information.
5. To verify the execution, check if the task completed (e.g., software installation or configuration changes) on the VM.
    - For example, if the script installs a package, you can check if it is installed by running the appropriate command (dpkg -l for Linux or checking Programs and Features for Windows).

### Task 3: Verify the Custom Script Execution

**Objective:** Ensure the custom script ran correctly and verify the changes made by the script.

**Instructions:**

1. Log in to the Virtual Machine either through SSH (for Linux) or RDP (for Windows).
2. Check if the script's intended task was successfully completed:
    - If it was a software installation, verify the software is present (use the command dpkg -l on Linux or check the Programs and Features on Windows).
    - If it modified configuration files, ensure the files were updated as expected.
3. Take a screenshot showing the successful execution and changes made by the custom script.

### Task 4: Troubleshoot Custom Script Execution (If Necessary)

**Objective:** Troubleshoot and resolve any issues with the execution of the custom script.

**Instructions:**

1. If the script did not run successfully, navigate back to the Extensions + applications section in the Azure Portal.
2. Click on the Custom Script Extension to view the logs.
3. Review the error messages to identify the issue (e.g., permission errors, incorrect script syntax).
4. Fix the issue in the script or environment and rerun the extension if needed.
5. Once the script runs successfully, confirm that the intended changes have been made on the VM.

## Submission Guidelines

- Submit a screenshot showing the Custom Script Extension installed and the execution status.
- Include a brief explanation of what the script was intended to do and any issues encountered during the process (if applicable).
- Upload the screenshot and description to the designated submission portal.

## Additional Resources

- [Azure Documentation: Custom Script Extensions for Linux VMs](https://docs.microsoft.com/azure/virtual-machines/extensions/custom-script-linux)
- [Azure Documentation: Custom Script Extensions for Windows VMs](https://docs.microsoft.com/azure/virtual-machines/extensions/custom-script-windows)
