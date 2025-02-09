# Lab Title: Integrating SonarQube with Azure DevOps for Automated Code Analysis

## Lab Overview

This lab guides you through setting up a SonarQube server, integrating it with Azure DevOps, and configuring a pipeline to perform automated code analysis. This integration will help maintain code quality and security by identifying issues early in the development process.

## Pre-requisites

- An active Azure DevOps account
- Administrative access to Azure DevOps project settings
- A project in Azure DevOps with a repository containing your source code
- Basic knowledge of Docker and CI/CD pipelines

## Learning Objectives

By the end of this lab, you will be able to:

- Set up a SonarQube server using Docker
- Integrate SonarQube with Azure DevOps
- Configure an Azure DevOps pipeline to include SonarQube analysis
- Analyze code quality and security issues using SonarQube reports

## Description

This lab provides a step-by-step process to set up a SonarQube server and integrate it with Azure DevOps. You will configure a service connection in Azure DevOps to communicate with SonarQube and modify your build pipeline to include code analysis steps. Finally, you will review the analysis results in SonarQube to identify and address code quality and security issues.

## Tasks

### Task 1: Set Up a Virtual Machine (VM) for SonarQube

**Objective:** Provision a VM to host the SonarQube server.

**Instructions:**

1. **Provision the VM:**
    - Create a new VM with the following specifications:
        - Operating System: Ubuntu 22.04 LTS
        - Instance Type: t2.medium or equivalent (2 vCPUs, 4 GB RAM)
        - Storage: At least 20 GB
    ![alt text](<Screenshot 2025-02-08 012127.png>)

2. **Ensure external access to the SonarQube web interface.**

**Instructions:**

1. **Modify Security Group or Firewall Settings:**
    - In your cloud provider's console, navigate to the security settings for your VM.
    - Add an inbound rule to allow traffic on port 9000.

**Verification:**

- Confirm that you can access `http://<VM_IP>:9000` from your local machine's browser.

    ![alt text](<Screenshot 2025-02-08 013842-networksettings.png>)
    ![alt text](<Screenshot 2025-02-08 013942-inboundrule.png>)
    ![alt text](<Screenshot 2025-02-08 014052.png>)
**Verification:**

- Confirm that the VM is running and accessible via SSH.
  ![alt text](<Screenshot 2025-02-08 012445.png>)

### Task 2: Install Docker on the VM

**Objective:** Set up Docker to run the SonarQube container.

**Instructions:**

1. **Update the Package List:**
    - Connect to the VM via SSH.
    - Run the following commands:
        ```bash
        sudo apt update
        sudo apt upgrade -y
        ```

2. **Install Docker:**
    - Run the following command:
        ```bash
        sudo apt install docker.io -y
        ```

3. **Add User to Docker Group:**
    - Run the following command:
        ```bash
        sudo usermod -aG docker $USER
        ```
    - Log out and log back in to apply the changes.

4. **Verify Docker Installation and Status:**
    - Run the following command:
        ```bash
        docker --version
        sudo systemctl status docker
        ```
    - Ensure the Docker version is displayed and status is actived.
    ![alt text](<Screenshot 2025-02-08 013518.png>)

**Verification:**

- Execute `docker ps` to ensure Docker is running without errors.
  ![alt text](<Screenshot 2025-02-08 013617.png>)

### Task 3: Deploy SonarQube Using Docker

**Objective:** Run the SonarQube container.

**Instructions:**

1. **Pull and Run SonarQube Docker Image:**
    - Run the following command:
        ```bash
        docker run -d --name sonarqube -p 9000:9000 sonarqube:lts-community
        ```
    ![alt text](<Screenshot 2025-02-08 014157.png>)
2. **Check the Running Container:**
    - Run the following command:
        ```bash
        docker ps -a
        ```
    - Ensure the SonarQube container is up and running.

**Verification:**

- Access the SonarQube web interface by navigating to `http://<VM_IP>:9000` in your browser.
    ![alt text](<Screenshot 2025-02-08 014245.png>)
- Log in with the default credentials:
    - Username: `admin`
    - Password: `admin`
- Upon first login, you'll be prompted to change the default password.
    ![alt text](<Screenshot 2025-02-08 022328.png>)
    ![alt text](<Screenshot 2025-02-08 022351.png>)
    ![alt text](<Screenshot 2025-02-08 022406.png>)

### Task 4: Integrate SonarQube with Azure DevOps

**Objective:** Configure Azure DevOps to connect with your SonarQube instance, enabling automated code analysis during your CI/CD pipelines.

**Instructions:**

1. **Install the SonarQube Extension in Azure DevOps:**
    - Navigate to the Azure DevOps Marketplace.
    - Search for "SonarQube" and select the official SonarQube extension.
    - Click "Get it free" and follow the prompts to install the extension to your Azure DevOps organization.
    ![alt text](<Screenshot 2025-02-08 024146.png>)
    ![alt text](<Screenshot 2025-02-08 024204.png>)
2. **Create a Service Connection to SonarQube:**
    - In Azure DevOps, go to your project and select Project Settings.
    - Under Pipelines, select Service connections.
    ![alt text](<Screenshot 2025-02-08 025620.png>)
    - Click New service connection and choose SonarQube.
    ![alt text](<Screenshot 2025-02-08 025636.png>)
    - Provide the following details:
        - Server URL: Enter your SonarQube server URL (e.g., `http://<VM_IP>:9000`).
        - Authentication Token: Use the token you generated in SonarQube.
3.  **Generate a Token in SonarQube:**
    1. Open your browser and log in to your SonarQube instance.
    2. Click on your profile icon and select **My Account**.
    3. Navigate to the **Security** section.
    4. Under **Tokens**, click **Generate Tokens**.
    5. Provide a descriptive name (e.g., "Azure DevOps Integration") and select default permissions.
    6. Click **Generate** and copy the token. Save it securely.
   ![alt text](<Screenshot 2025-02-08 025935.png>)
   ![alt text](<Screenshot 2025-02-08 030052.png>)
   
        - Service Connection Name: Enter a descriptive name.
    - Click Save.

4. **Configure Your Azure Pipeline for SonarQube Analysis:**
    - Navigate to your Azure DevOps project and select Pipelines.
    - Edit the pipeline associated with the project you want to analyze.
    - Add the **Prepare Analysis Configuration** task:
        - Click `+` to add a new task.
        - Search for SonarQube and select **Prepare Analysis Configuration**.
        - Configure the task:
            - SonarQube Server Endpoint: Select the service connection created earlier.
            - Project Key: Enter the unique project key in SonarQube.
            - Project Name: Enter the project name as defined in SonarQube.
    - Ensure the **Prepare Analysis Configuration** task is placed before your build tasks.
    - Add the **Run Code Analysis** task after your build tasks.
    - Add the **Publish Quality Gate Result** task to display the Quality Gate status.
    - Save and queue the pipeline.
    ![alt text](<Screenshot 2025-02-08 030557.png>)

**Verification:**

- Upon pipeline completion, check the build summary.
- Review the **SonarQube Analysis Report** section for Quality Gate status.
- Access detailed results via the provided link.

## Submission Guidelines

- Provide a screenshot of the running SonarQube container.
- Include confirmation of SonarQube web interface access.
- Attach the pipeline execution summary showing analysis results.
- Submit a brief report highlighting key learnings and challenges faced.

## Additional Resources

- [SonarQube Documentation](https://docs.sonarqube.org/)
- [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/)
- [Docker Documentation](https://docs.docker.com/)
- [SonarQube Azure DevOps Integration](https://www.sonarqube.org/azure-devops/)

