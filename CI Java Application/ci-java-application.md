# Continuous Integration for a Java Application Covering Build, Test, Scan, and Publishing Artifact via Azure DevOps (Classic Pipeline)

## Lab Overview
In this lab, you will learn how to set up and execute a complete Continuous Integration (CI) pipeline for a Java application using Azure DevOps Classic Pipeline. You will build the application, run code scans, and publish build artifacts. By the end of this lab, you'll have a hands-on understanding of how to create and manage a CI pipeline for reliable and efficient software delivery.

## Pre-requisites
- An Azure DevOps account with access to an organization and project.
- Java Development Kit (JDK) installed.
- Maven installed.
- Access to an existing SonarQube instance.
- Permissions to create service connections and pipelines in Azure DevOps.
- Make sure you have the application code on Azure Repo (https://github.com/srahul0502/Ekart.git).


## Learning Objectives
By completing this lab, you will:
1. Understand how to create a CI pipeline using Azure DevOps Classic Pipeline.
2. Build, scan, and publish artifacts for a Java application.
3. Utilize Maven and SonarQube for build and code quality checks.

## Description
In this guided lab, you will follow a step-by-step approach to:
- Set up essential service connections.
- Configure tasks to build the application, run code scans, and publish artifacts.
- Verify each task and ensure successful execution of the pipeline.

## Tasks

### Task 1: Create an ARM Service Connection
**Objective:** Set up an Azure Resource Manager (ARM) service connection.

**Instructions:**
1. Navigate to **https://dev.azure.com** and select your organization and project.
2. Go to **Project Settings** > under **pipelines** > **Service Connections**.
   ![alt text](<Screenshot 2025-02-08 032604.png>)
3. Click **New Service Connection**.
   ![alt text](<Screenshot 2025-02-08 032611.png>)
4. Select **Azure Resource Manager**.
5. Choose **Service principal (automatic)** and click **Next**.
6. Select the appropriate subscription and resource group.
7. Provide a meaningful name for the service connection (e.g., "ARM").
8. Click **Verify and Save**.

   ![alt text](<Screenshot 2025-02-08 032447.png>)

**Verification:**
- Ensure the service connection is successfully created and listed under service connections.

### Task 2: Create a SonarQube Service Connection
**Objective:** Use the existing SonarQube instance for code analysis.

**Instructions:**
1. Navigate to **Project Settings** > under **pipelines** > **Service Connections**.
2. Click **New Service Connection**.
3. Select **SonarQube** and click **Next**.
4. Enter the required details:
   - **Server URL:** URL of your SonarQube instance. (Please refer to "Setting up SonarQube Lab )
   - **Authentication Token:** Provide a token generated in SonarQube.

**Generate a Token in SonarQube:**
1. Open your browser and log in to your SonarQube instance.
2. Click on your profile icon and select **My Account**.
3. Navigate to the **Security** section.
4. Under **Tokens**, click **Generate Tokens**.
5. Provide a descriptive name (e.g., "Azure DevOps Integration") and select default permissions.
6. Click **Generate** and copy the token. Save it securely.
   ![alt text](<Screenshot 2025-02-08 025935.png>)
   ![alt text](<Screenshot 2025-02-08 030052.png>)
   

7. Provide a name for the service connection (e.g., "Sonar").
8. Click **Verify and Save**.
   ![alt text](<Screenshot 2025-02-08 030114.png>)

**Verification:**
- Ensure the service connection is successfully created and listed.

### Task 3: Set Up the Pipeline
**Objective:** Create and configure a Classic Pipeline for the Java application.

**Instructions:**
1. Navigate to **Pipelines** > **Create Pipeline**.
   ![alt text](<Screenshot 2025-02-08 030324.png>)
2. Select **Classic Editor**.
3. Choose your repository and click **Continue**.
4. Select **Empty Job**.
      ![alt text](<Screenshot 2025-02-08 030337.png>)
5. Configure tasks as follows:

#### Step 1: Configure the Maven Task
**Objective:** Build the Java application.

**Instructions:**
1. Drag and drop the **Maven** task from the task assistant.
   ![alt text](<Screenshot 2025-02-08 030351.png>)
2. Set the following properties:
   - **Display Name:** Maven pom.xml
   - **Goals:** package -DskipTests=True
   - **Azure Subscription:** Select the ARM service connection.

#### Step 2: Copy Files Task
**Objective:** Copy build artifacts to the staging directory.

**Instructions:**
1. Drag and drop the **Copy Files** task from the task assistant.
2. Configure the task as follows:
   - **Source Folder:** $(system.defaultworkingdirectory)
   - **Contents:** **/*.jar
   - **Target Folder:** $(build.artifactstagingdirectory)

#### Step 3: Publish Build Artifacts Task
**Objective:** Publish build artifacts.

**Instructions:**
1. Drag and drop the **Publish Build Artifacts** task from the task assistant.
2. Set the Display Name to "Publish Artifact: drop".

#### Step 4: Prepare SonarQube Analysis
**Objective:** Configure SonarQube analysis for the project.

**Instructions:**
1. Drag and drop the "Prepare analysis on SonarQube Server" task from the task assistant.
2. Configure the task:
   - **Display Name:** Prepare analysis on SonarQube Server
   - **SonarQube Server Endpoint:** Click on **New** to create a SonarQube server endpoint.
   - **Token:** To generate a token, go to your SonarQube server, click **My Account > Security > Generate Tokens**, and save the token.
   - **Scanner Mode:** CLI
   - **Configuration Mode:** Manual
   - **CLI Project Key:** shopping
   - **CLI Project Name:** EKart
   - **Extra Properties:** sonar.java.binaries=.

#### Step 5: SonarQube Analyze Task
**Objective:** Run code analysis.

**Instructions:**
1. Drag and drop the **SonarQube Analyze** task from the task assistant.
2. Set the Display Name to "Run Code Analysis".
3. to check the analysis result navigate to sonarqube instance > project.
   ![alt text](<Screenshot 2025-02-08 041614.png>)

#### Step 6: Dependency Check Task
**Objective:** Perform a dependency check and generate reports.

**Instructions:**
1. Drag and drop the **Dependency Check** task from the task assistant.
2. Configure as follows:
   - **Project Name:** EKart
   - **Scan Path:** .
   - **Upload SARIF Report:** true

#### Step 7: Archive and Publish Build Artifacts
**Objective:** Archive and publish build artifacts.

**Instructions:**
1. Drag and drop the **Archive Files** task.
2. Set Display Name to "Archive $(build.artifactstagingdirectory)".
3. Set the root folder to $(build.artifactstagingdirectory).
4. Enable "Include Root Folder".
5. Drag and drop the **Publish Build Artifacts** task.
6. Set Display Name to "Publish Artifact".
7. Set the path to publish as $(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip.
8. Set the artifact name to $(Parameters.ArtifactName).
   ![alt text](<Screenshot 2025-02-08 034455.png>)
   ![alt text](<Screenshot 2025-02-08 041238.png>)
   ![alt text](<Screenshot 2025-02-08 041251.png>)

**Verification:**
- Confirm that artifacts are successfully published.

### Task 4: Run the Pipeline
**Objective:** Execute the pipeline and verify all steps.

**Instructions:**
1. Click **Save and Queue**.
2. Choose the appropriate agent pool and specification.
   ![alt text](<Screenshot 2025-02-08 033501.png>)
3. Enable system diagnostics.
4. Click **Run**.
   ![alt text](<Screenshot 2025-02-08 033536.png>)

**Verification:**
- Ensure two artifacts are produced:
  - One containing the dependency check HTML file.
  - The other containing the Java application.
- Navigate to **SonarQube > Project** to view the code analysis results.

## Submission Guidelines
- Provide a screenshot of the successful pipeline run.
- Include screenshots showing the generated artifacts.
- Attach the SonarQube analysis result page.

## Additional Resources
- [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/)
- [Maven Documentation](https://maven.apache.org/)
- [SonarQube Documentation](https://www.sonarqube.org/)

