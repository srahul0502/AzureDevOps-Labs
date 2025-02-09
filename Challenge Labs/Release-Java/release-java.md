# **Challenge Lab: Setup Release pipeline to deploy application a java application (as a docker container) on a web app **

## **Lab Overview**
This challenge lab requires you to set up a complete release pipeline to deploy a Dockerized Java application on an Azure Web App using Azure DevOps.

## **Pre-requisites**
- Basic knowledge of Docker and Azure DevOps.
- An Azure account with necessary permissions.
- A Java-based application ready for containerization.
- Installed Docker CLI and Maven.
- **Clone the repository to local and Azure Repos** (https://github.com/srahul0502/Ekart.git)

## **Learning Objectives**
- Build and test Docker images locally.
- Configure and push Docker images to Azure Container Registry (ACR).
- Deploy the containerized application to an Azure Web App.
- Automate quality analysis with SonarQube.

## **Description**
In this challenge lab, you will complete a series of tasks to build, containerize, and deploy a Java-based web application using Azure DevOps. You must perform each task efficiently and verify successful completion.

## **Tasks**

### **Task 1: Test Dockerfile Locally**
#### **Objective:** Test the existing Dockerfile for the Java application.
#### **Instructions:**
1. Ensure the Dockerfile is present in your project root directory.
2. Build the Docker image:
   ```bash
   docker build -t your-application:latest .
   ```
3. Run the container locally:
   ```bash
   docker run -p 8080:8080 your-application:latest
   ```
4. Visit `http://localhost:8080` to verify it’s working.
#### **Verification:**
- Ensure the application is accessible at `http://localhost:8080`.

---

### **Task 2: Configure Azure Container Registry (ACR)**
#### **Objective:** Create and configure an ACR instance.
#### **Instructions:**
1. Navigate to **Create a resource > Containers > Container Registry** in the Azure Portal.
2. Provide the necessary information:
   - **Registry Name:** A unique name for your registry.
   - **Subscription:** Select your subscription.
   - **Resource Group:** Choose or create a new resource group.
   - **Location:** Select the preferred location.
3. Click **Review + create**, then **Create**.
4. Enable the Admin User:
   - Go to the **Access Keys** section of your registry.
   - Set **Admin user** to **Enabled**.
   - Note the **Username** and **Password** for later use.
#### **Verification:**
- Confirm that the ACR instance is created and accessible from the Azure Portal.

---

### **Task 3: Configure CI Pipeline in Azure DevOps**
#### **Objective:** Automate the process of building and pushing Docker images to ACR.
#### **Instructions:**
1. Navigate to **Pipelines > New Pipeline** in Azure DevOps.  
2. Select your code repository.  
3. Drag and drop the following tasks from the task assistant:  

### Step 1: Maven  
- **Display Name:** Build with Maven  
- **Maven Pom File:** `pom.xml`  
- **Goals:** `package`  

### Step 2: Docker  
- **Display Name:** Build and Push Docker Image  
- **Container Registry:** `your-acr-connection`  
- **Repository:** `$(imageName)`  
- **Command:** `buildAndPush`  
- **Dockerfile:** `**/Dockerfile`  
- **Tags:** `$(Build.BuildId)`  

4. Save and run the pipeline.  
#### **Verification:**
- Ensure that the Docker image is successfully pushed to ACR.
  ![alt text](<Screenshot 2025-02-08 074211-acrrrrrfinal.png>)

---

### **Task 4: Prepare SonarQube Analysis**
#### **Objective:** Configure SonarQube analysis for the project.
#### **Instructions:**
1. Navigate to **Pipelines > Releases** in Azure DevOps.
2. Drag and drop the "Prepare analysis on SonarQube Server" task from the task assistant.
3. Configure the task:
   - **Display Name:** Prepare analysis on SonarQube Server
   - **SonarQube Server Endpoint:** Click on New to create a SonarQube server endpoint.
   - **Token:** To generate a token, go to your SonarQube server, click **My Account > Security > Generate Tokens**, and save the token.
   - **Scanner Mode:** CLI
   - **Configuration Mode:** Manual
   - **CLI Project Key:** webapplication
   - **CLI Project Name:** WebApplication
#### **Verification:**
- Ensure that SonarQube analysis runs successfully without errors.

---

### **Task 5: Create Azure Web App for Containers**
#### **Objective:** Set up a web app in Azure to host your containerized application.
#### **Instructions:**
1. In the Azure Portal, go to **Create a resource > Web > Web App for Containers**.
2. Configure the following:
   - **Subscription:** Select your subscription.
   - **Resource Group:** Choose the appropriate resource group.
   - **Name:** Provide a unique name for your web app.
   - **Operating System:** Linux.
3. In the **Docker** tab:
   - Select **Azure Container Registry** as the image source.
   - Choose your ACR instance.
   - Select the appropriate repository and tag.
4. Click **Review + create**, then **Create**.
   
   ![alt text](<Screenshot 2025-02-08 045109.png>)

#### **Verification:**
- Confirm that the web app is deployed and accessible.

---

### **Task 6: Configure Release Pipeline**
#### **Objective:** Automate the deployment of Docker images to Azure Web App.
#### **Instructions:**
1. Navigate to **Pipelines > Releases** in Azure DevOps.
2. Click **New pipeline**.
3. Select **Azure App Service deployment** and click **Apply**.
4. Rename the default stage to **Production**.
5. Add an artifact:
   - **Source type:** Select **Build**.
   - **Project:** Choose your current project.
   - **Source:** Select the CI pipeline.
6. Configure the deployment task:
   - Click **Tasks** under the **Production** stage.
   - Select the **Azure Web App for Containers** task.
   - Fill in the following details:
     - **Azure Subscription:** Select your subscription and authorize if needed.
     - **App Service Name:** Choose the web app you created.
     - **Image Name:** Specify the full image path from ACR.
     - **Tag:** Specify the image tag.
7. Save and create a release.
8. Monitor the deployment process.
#### **Verification:**
- Ensure that the deployment is successful and the application is accessible from the web app URL.

---

## **Submission Guidelines**
- Submit screenshots of the following:
  - Successful Docker image build and run locally.
  - ACR configuration with the pushed Docker image.
  - Successful SonarQube analysis.
  - Azure Web App running the containerized application.
  - Successful release pipeline execution.

## **Additional Resources**
- [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops)
- [Docker Documentation](https://docs.docker.com/)
- [SonarQube Documentation](https://docs.sonarqube.org/)

