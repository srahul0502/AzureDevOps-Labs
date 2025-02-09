**Lab Title: Setting Up a Release Pipeline to Deploy a .NET Application to an Azure Web App**

## **Lab Overview**
In this lab, you will learn how to create a release pipeline in Azure DevOps to deploy a .NET application to an Azure Web App. By the end of the lab, you will have a fully configured and functional release pipeline.

## **Pre-requisites**
- An Azure subscription with a provisioned App Service for .NET hosting.
- An Azure DevOps project with build artifacts ready for deployment.
- A service connection in Azure DevOps to authenticate with Azure.

## **Learning Objective**
By completing this lab, you will be able to:
- Create and configure a release pipeline in Azure DevOps.
- Deploy a .NET application to an Azure Web App.
- Monitor and verify deployment success.

## **Description**
This lab guides you through the process of setting up and configuring a release pipeline in Azure DevOps for deploying .NET applications to Azure Web Apps. You will learn how to create the necessary Azure resources, set up deployment tasks, and verify the deployment.

## **Tasks**

### **Task 1: Create the Web App**
#### Objective
Provision an Azure Web App for hosting your .NET application.

#### Instruction
1. In the Azure portal search bar, type **App Services** and select it.
2. Click **Create**, then select **Web App** from the available templates.
3. Fill in the following fields:
    - **Subscription:** Select your Azure subscription.
    - **Resource Group:** Select the resource group created earlier.
    - **Name:** Enter a globally unique name for your app (e.g., *myapp123*).
    - **Publish:** Select **Code**.
    - **Runtime Stack:** Choose **.NET 6**, **.NET 5**, or **.NET Core 3.1** depending on your application.
    - **Operating System:** Choose **Windows** (or **Linux** if preferred).
    - **Region:** Select the same region as your App Service Plan.
    - **App Service Plan:** Select the previously created App Service Plan.
4. Click **Next: Deployment >** and skip if not using deployment options.
5. Click **Next: Monitoring >** and configure Application Insights if desired.
6. Click **Review + Create**, then **Create**.
    ![alt text](<Screenshot 2025-02-09 021218.png>)

#### Verification
Ensure that the Web App is created successfully by navigating to the App Services section in the Azure portal.

### **Task 2: Create the Release Pipeline**
#### Objective
Set up a release pipeline in Azure DevOps to deploy a .NET application.

#### Instruction
1. Go to Azure DevOps and navigate to the project.
2. Select **Pipelines > Releases**, then click **New Pipeline**.

#### Verification
Verify that the release pipeline is created and listed under Releases.

### **Task 3: Configure Pipeline Stages**
#### Objective
Configure stages and artifacts for the release pipeline.

#### Instruction
1. Choose **Empty Job** for a clean setup.
2. Name the stage (e.g., *Deploy to Azure Web App*).
3. Click **Add an artifact:**
    - Select the build pipeline that contains your .NET application.
    - Set the default version to **Latest**.
    - Click **Add**.

#### Verification
Ensure that the artifact is successfully added to the pipeline.

### **Task 4: Set up Deployment Task**
#### Objective
Add deployment tasks to the release pipeline.

#### Instruction
1. Select the stage you created and click on **Tasks**.
2. Click **Agent job** and choose **Azure Pipelines** for the Agent pool.
3. Add a new task:
    - Search for **Azure App Service Deploy** and click **Add**.
4. Configure the task:
    - **Azure Subscription:** Select your service connection.
    - **App Service Type:** Choose **Web App on Windows** or **Web App on Linux** depending on your setup.
    - **App Service Name:** Select your provisioned App Service.
    - **Package or Folder:** Point to the build artifact (`$(System.DefaultWorkingDirectory)/<artifact-name>.zip`).
    - Leave default values unless your app has specific configurations.
    ![alt text](<Screenshot 2025-02-09 021450.png>)

#### Verification
Ensure that the deployment task is configured and saved without errors.

### **Task 5: Set Deployment Slot (Optional)**
#### Objective
Deploy to a specific deployment slot.

#### Instruction
1. Enable the **Deployment Slot** option and select the desired slot.

#### Verification
Ensure that the deployment slot configuration is saved correctly.

### **Task 6: Configure Environment Variables (Optional)**
#### Objective
Set application configuration values.

#### Instruction
1. Add an **App Settings and Configuration Variables** section in the deployment task.
2. Provide key-value pairs directly.

#### Verification
Verify that environment variables are set correctly in the pipeline configuration.

### **Task 7: Save and Create Release**
#### Objective
Trigger the deployment process.

#### Instruction
1. Click **Save** and provide a commit message.
2. Select **Create Release** and link the pipeline artifact.
3. Start the release by clicking **Deploy**.
    ![alt text](<Screenshot 2025-02-09 021907.png>)
    ![alt text](<Screenshot 2025-02-09 021836.png>)

#### Verification
Ensure that the release deployment starts without errors.

### **Task 8: Monitor the Deployment**
#### Objective
Track deployment progress.

#### Instruction
1. Check the logs to monitor the deployment status in **Logs**.
2. Look for success indicators or troubleshoot errors if deployment fails.

#### Verification
Ensure that the deployment completes successfully.

### **Task 9: Verify the Deployment**
#### Objective
Confirm the successful deployment of the application.

#### Instruction
1. Open the Azure portal and navigate to the deployed App Service.
2. Verify that the application is running correctly by accessing the web app’s public URL.
   
   ![alt text](<Screenshot 2025-02-09 021847.png>)
   

#### Verification
Ensure the application is accessible and functioning as expected.
    ![alt text](<Screenshot 2025-02-09 021821.png>)

## **Submission Guidelines**
- Provide screenshots of the completed tasks, including the deployment pipeline, successful deployment logs, and the running web application.
- Submit a report summarizing the steps taken, any challenges faced, and their resolutions.

## **Additional Resources**
- [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/)
- [Azure App Service Documentation](https://learn.microsoft.com/en-us/azure/app-service/)

