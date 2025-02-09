# Continuous Integration for a .NET Application Covering Build, Test, Scan, and Publishing Artifact via Azure DevOps

## Lab Overview
In this lab, you will learn how to set up and execute a complete Continuous Integration (CI) pipeline for a .NET application using Azure DevOps. You will build the solution, run automated tests, perform code scanning using SonarQube, and publish build artifacts. By the end of this lab, you'll have a hands-on understanding of how to create and manage a CI pipeline for reliable and efficient software delivery.

## Pre-requisites
- An Azure DevOps account.
- Basic familiarity with Azure DevOps concepts.
- A sample .NET solution.
- A SonarQube instance running on a virtual machine.

## Learning Objectives
By completing this lab, you will:
1. Clone a repository into Azure DevOps.
2. Create a classic pipeline with Azure DevOps.
3. Configure tasks to build, test, and analyze the solution.
4. Publish build artifacts.

## Description
In this guided lab, you will follow a step-by-step approach to:
- Set up the build environment.
- Build the application and run tests.
- Analyze code quality using SonarQube.
- Archive and publish build artifacts.
- Verify each step to ensure a successful pipeline execution.

## Tasks

### Task 1: Clone the Repository
**Objective:** Set up your project repository in Azure DevOps.

**Instructions:**
1. Go to your Azure DevOps account and create a new project.
2. Navigate to Repos > Import Repository(https://github.com/srahul0502/WebApplication.git).
3. Provide the URL of your .NET application repository or manually upload your code.
4. Confirm the import.

**Verification:**
- Verify that your code is visible in Azure DevOps under Repos.

### Task 2: Create a Classic Pipeline
**Objective:** Build a CI pipeline using the classic editor in Azure DevOps.

**Instructions:**
1. Go to Pipelines > New Pipeline.
2. Select "Use the classic editor" to create the pipeline.
3. Choose the repository you imported.
4. Select "Empty job" to start with a blank pipeline.

**Verification:**
- Verify that the pipeline editor opens with an empty job.

### Task 3: Configure Pipeline Tasks

#### Step 1: Use NuGet Tool Installer
**Objective:** Install the latest version of NuGet.

**Instructions:**
1. Drag and drop the "NuGet Tool Installer" task from the task assistant.
2. Set Display Name to "Use NuGet".
3. Enable "Check Latest Version".
4. Save the configuration.

**Verification:**
- Verify that the task appears in the pipeline configuration.

#### Step 2: Build the Solution
**Objective:** Build the .NET solution.

**Instructions:**
1. Drag and drop the "Visual Studio Build" task.
2. Configure the task:
    - **Solution:** $/Azure DevOps Basics/Basics/WebApplication/WebApplication.sln
    - **MSBuild Arguments:** /p:DeployOnBuild=True /p:DeployDefaultTarget=WebPublish /p:WebPublishMethod=FileSystem /p:publishUrl=$(build.ArtifactStagingdirectory)
    - **Clean:** true
    - **Restore NuGet Packages:** true
    - **MSBuild Architecture:** x64
    - **Create Log File:** true
3. Save the task configuration.

**Verification:**
- Verify that the solution builds without errors.

#### Step 3: Run Unit Tests
**Objective:** Execute unit tests for the solution.

**Instructions:**
1. Drag and drop the "DotNetCoreCLI" task.
2. Configure the task:
    - **Display Name:** dotnet test
    - **Command:** test
    - **Project Path:** TestProject/TestProject.csproj
    - **Arguments:** --no-build --verbosity normal
    - **Working Directory:** $\Azure DevOps Basics\Basics\WebApplication
    - **Continue On Error:** true
3. Save the task configuration.

**Verification:**
- Check the test results for successful execution.

#### Step 4: Prepare SonarQube Analysis
**Objective:** Configure SonarQube analysis for the project.

**Instructions:**
1. Drag and drop the "Prepare analysis on SonarQube Server" task from the task assistant.
2. Configure the task:
    - **Display Name:** Prepare analysis on SonarQube Server
    - **SonarQube Server Endpoint:** Click on New to create a SonarQube server endpoint.
    - **Token:** To generate a token, go to your SonarQube server, click My Account > Security > Generate Tokens, and save the token.
    - **Scanner Mode:** CLI
    - **Configuration Mode:** Manual
    - **CLI Project Key:** webapplication
    - **CLI Project Name:** WebApplication
3. Save the task configuration.

**Verification:**
- Ensure the task is configured and linked to the SonarQube server.

#### Step 5: Analyze the Code
**Objective:** Execute SonarQube analysis.

**Instructions:**
1. Drag and drop the "Run Code Analysis" task.
2. Set Display Name to "Run Code Analysis".

**Verification:**
- Check the SonarQube server (VM) under Projects to view analysis results.
    ![alt text](<Screenshot 2025-02-09 013311.png>)

#### Step 6: Archive and Publish Build Artifacts
**Objective:** Archive and publish build artifacts.

**Instructions:**
1. Drag and drop the "Archive Files" task.
2. Set Display Name to "Archive $(build.artifactstagingdirectory)".
3. Set the root folder to $(build.artifactstagingdirectory).
4. Enable "Include Root Folder".
5. Drag and drop the "Publish Build Artifacts" task.
6. Set Display Name to "Publish Artifact".
7. Set the path to publish as $(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip.
8. Set the artifact name to $(Parameters.ArtifactName).

**Verification:**
- Confirm that artifacts are successfully published.
    ![alt text](<Screenshot 2025-02-09 013129.png>)
    ![alt text](<Screenshot 2025-02-09 012728.png>)
### Task 4: Run the Pipeline
**Objective:** Execute the pipeline and verify all steps.

**Instructions:**
1. Click Save and Queue.
2. Choose the appropriate agent pool and specification.
3. Enable system diagnostics.
4. Click Run.

**Verification:**
- Ensure the pipeline completes without errors.
- Verify that build artifacts are available.
- Confirm that SonarQube analysis results are visible.

## Submission Guidelines
- Provide a screenshot of the successful pipeline run.
- Include screenshots of build artifacts and SonarQube analysis results.
- Submit the link to the Azure DevOps project.

## Additional Resources
- [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/?view=azure-devops)
- [SonarQube Documentation](https://docs.sonarqube.org/)
