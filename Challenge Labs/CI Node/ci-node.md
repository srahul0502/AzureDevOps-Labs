# Continuous Integration for a Node Application Covering Build, Test, Scan, and Publishing Artifact via Azure DevOps (Classic Pipeline)

## Lab Overview
In this lab, you will learn how to set up and execute a complete Continuous Integration (CI) pipeline for a Node application using Azure DevOps Classic Pipeline. You will build the application, run code scans, and publish build artifacts. By the end of this lab, you'll have a hands-on understanding of how to create and manage a CI pipeline for reliable and efficient software delivery.

## Pre-requisites
- Azure DevOps account
- Basic knowledge of Node.js and package management
- A sample Node.js application repository (or use your own project)

## Learning Objectives
- Create a classic pipeline in Azure DevOps
- Build and test a Node.js application
- Perform static code analysis with SonarQube
- Publish build artifacts for deployment

## Description
This lab will guide you step by step through creating a fully functional CI pipeline for a Node.js application in Azure DevOps. You will learn how to automate building, testing, code scanning, and publishing artifacts.

## Tasks

### Task 1: Clone the Repository
**Objective:** Set up the project repository in Azure DevOps.

**Instructions:**
1. Navigate to Azure DevOps and select your project.
2. Go to Repos and select “Import a repository.”
3. Enter the repository URL or upload your Node.js application.
4. Click “Import” to clone the repository into Azure DevOps.

**Verification:**
- Ensure that the repository is available in Azure DevOps.

### Task 2: Create a Classic Pipeline
**Objective:** Set up a classic build pipeline for the Node.js application.

**Instructions:**
1. Navigate to Pipelines in Azure DevOps.
2. Select “New Pipeline” and choose “Use the classic editor.”
3. Select the repository you cloned.
4. Choose the appropriate agent pool for your build environment.
5. Save the initial pipeline.

**Verification:**
- Confirm that the pipeline is created and ready for task configuration.

### Task 3: Add Build Task
**Objective:** Use Node.js to install project dependencies and build the application.

**Instructions:**
1. Drag and drop the **Node Tool** task from the task assistant.
2. Configure the task:
   - Display Name: Use Node 16.x
   - Version Spec: 16.x
   - Check Latest: True
3. Drag and drop the **npm install** task.
4. Configure the task:
   - Working Directory: ./
   - Verbose: True

**Verification:**
- Save, queue, choose an agent, and run the pipeline.
- Check the logs for successful dependency installation and build completion.

### Task 4: Add Test Task
**Objective:** Run tests for the Node.js application.

**Instructions:**
1. Drag and drop the **npm custom command** task.
2. Configure the task:
   - Display Name: npm test
   - Command: Custom
   - Working Directory: ./
   - Custom Command: test test.js

**Verification:**
- Save, queue, choose an agent, and run the pipeline.
- Confirm that tests pass and results are logged.

### Task 5: Configure SonarQube Analysis
**Objective:** Perform static code analysis on the project.

**Instructions:**
1. Drag and drop the **Prepare analysis on SonarQube Server** task.
2. Configure the task:
   - Display Name: Prepare analysis on SonarQube Server
   - SonarQube Server Endpoint: Create a new endpoint if needed.
   - Scanner Mode: CLI
   - Configuration Mode: Manual
   - CLI Project Key: Node Application
   - CLI Project Name: Node Application
3. Drag and drop the **Run Code Analysis** task.
4. Configure the task:
   - Display Name: Run Code Analysis

**Verification:**
- Save, queue, choose an agent, and run the pipeline.
- Check the analysis results on the SonarQube server under your project.

### Task 6: Perform Dependency Check
**Objective:** Scan the application for security vulnerabilities.

**Instructions:**
1. Drag and drop the **Dependency Check** task.
2. Configure the task:
   - Display Name: Dependency Check
   - Project Name: Node Application
   - Scan Path: package.json

**Verification:**
- Save, queue, choose an agent, and run the pipeline.
- Confirm that the scan completes successfully and logs any vulnerabilities found.
  ![alt text](<Screenshot 2025-02-09 034208.png>)

### Task 7: Publish Build Artifacts
**Objective:** Prepare and publish artifacts for deployment.

**Instructions:**
1. Drag and drop the **Copy Files** task.
2. Configure the task:
   - Display Name: Copy Files
   - Source Folder: $(Build.SourcesDirectory)
   - Contents: **/*.js, **/*.json
   - Target Folder: $(Build.ArtifactStagingDirectory)
3. Drag and drop the **Archive Files** task.
4. Drag and drop the **Publish Build Artifacts** task.
5. Configure the task:
   - Display Name: Publish Artifact: drop

**Verification:**
- Save, queue, choose an agent, and run the pipeline.
- Ensure the artifacts are published and accessible in Azure DevOps.

## Submission Guidelines
1. Ensure the pipeline runs successfully without errors.
2. Provide screenshots of the completed pipeline runs for each task.
3. Verify and document the SonarQube analysis results.
4. Submit a report summarizing the steps, observations, and outcomes.

## Additional Resources
- [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/)
- [Node.js Documentation](https://nodejs.org/en/docs/)
- [SonarQube Documentation](https://docs.sonarqube.org/)

