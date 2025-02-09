# **Challenge:Release pipeline to deploy application a java application (as a docker container) on a web app **

## **Common Challenges and Tips**

1. **Docker Build and Run Errors:**
   - Incorrect Dockerfile configurations may lead to build failures.
   - **Tip:** Ensure the Dockerfile is at the project root and uses an appropriate base image for the Java application.

2. **Authentication Issues with ACR:**
   - Forgetting to enable Admin User or configure correct credentials can cause authentication problems.
   - **Tip:** Enable the Admin User in ACR and use the correct username and password.

3. **Pipeline Configuration Errors:**
   - Missing environment variables or misconfigured tasks may cause pipeline failures.
   - **Tip:** Properly configure Maven and Docker tasks with required variables.

4. **SonarQube Integration Issues:**
   - Token-related errors or incorrect server configurations can occur.
   - **Tip:** Ensure proper token generation and correct server endpoint setup.

5. **Deployment Issues to Azure Web App:**
   - Selecting incorrect Docker image paths or tags during release pipeline configuration.
   - **Tip:** Verify the image path and tag information in ACR.

6. **Release Pipeline Errors:**
   - Deployment errors may arise if App Service configurations are incorrect.
   - **Tip:** Confirm the App Service is configured for Linux and the correct image source is selected.

---

## **Submission Checklist**

- **Screenshots:**
  - Docker image build and local run verification.
  - ACR configuration with pushed Docker image.
  - SonarQube analysis.
  - Azure Web App running the containerized application.
  - Successful release pipeline execution.

- **Reports:**
  - Verification steps and results for each task.
  - Encountered issues and resolutions.

---

## **Solution**

### **Step 1: Test Dockerfile Locally**

1. Open the terminal and navigate to the project root directory.
2. Build the Docker image:
   ```bash
   docker build -t your-application:latest .
   ```
3. Run the container locally:
   ```bash
   docker run -p 8080:8080 your-application:latest
   ```
4. Open a browser and visit `http://localhost:8080` to verify the application.

   💡 **Tip:** Expose the correct port in the Dockerfile.

---

### **Step 2: Configure Azure Container Registry (ACR)**

1. Navigate to **Azure Portal > Create a resource > Containers > Container Registry**.
2. Configure the following:
   - **Registry Name:** Unique name.
   - **Subscription:** Appropriate subscription.
   - **Resource Group:** Create or select an existing group.
   - **Location:** Preferred location.
3. Click **Review + create**, then **Create**.
4. Enable Admin User:
   - Go to **Access Keys** and enable **Admin user**.
   - Note down the **Username** and **Password**.

   💡 **Tip:** Highlight security considerations for Admin user feature.

---

### **Step 3: Configure CI Pipeline in Azure DevOps**

1. Navigate to **Azure DevOps > Pipelines > New Pipeline**.
2. Select your code repository.
3. Configure the following tasks:
   - **Maven Task:**
     - **Display Name:** Build with Maven
     - **Maven Pom File:** `pom.xml`
     - **Goals:** `package`
   - **Docker Task:**
     - **Display Name:** Build and Push Docker Image
     - **Container Registry:** Select ACR connection
     - **Repository:** `$(imageName)`
     - **Command:** `buildAndPush`
     - **Dockerfile:** `**/Dockerfile`
     - **Tags:** `$(Build.BuildId)`
4. Save and run the pipeline.

   💡 **Tip:** Create secure service connections to ACR.

---

### **Step 4: Prepare SonarQube Analysis**

1. Navigate to **Azure DevOps > Pipelines > Releases**.
2. Add the **Prepare analysis on SonarQube Server** task.
3. Configure the task:
   - **SonarQube Server Endpoint:** Create a new endpoint.
   - **Token:** Generate a token in SonarQube.
   - **Scanner Mode:** CLI
   - **Project Key:** `webapplication`
   - **Project Name:** `WebApplication`
4. Run the release pipeline.

   💡 **Tip:** Emphasize the importance of code quality.

---

### **Step 5: Create Azure Web App for Containers**

1. Navigate to **Azure Portal > Create a resource > Web > Web App for Containers**.
2. Configure:
   - **Subscription:** Select subscription.
   - **Resource Group:** Appropriate group.
   - **Name:** Unique name.
   - **Operating System:** Linux.
3. In the Docker tab:
   - Select **Azure Container Registry** as the image source.
   - Choose correct ACR instance.
   - Select repository and tag.
4. Click **Review + create**, then **Create**.

   💡 **Tip:** Explain container scaling and monitoring features.

---

### **Step 6: Configure Release Pipeline**

1. Navigate to **Azure DevOps > Pipelines > Releases**.
2. Click **New pipeline** and select **Azure App Service deployment**.
3. Rename the stage to **Production**.
4. Add an artifact:
   - **Source type:** Build
   - **Project:** Current project
   - **Source:** Select CI pipeline
5. Configure deployment task:
   - Select **Azure Web App for Containers** task.
   - Configure:
     - **Azure Subscription:** Select and authorize.
     - **App Service Name:** Select web app.
     - **Image Name:** Specify full image path from ACR.
     - **Tag:** Specify image tag.
6. Save and create release.
7. Monitor deployment.

   💡 **Tip:** Use deployment slots for production scenarios.

---

## **Verification Tips**

- **Docker Build and Run:** Ensure successful local build and application access.
- **ACR Configuration:** Confirm image push in ACR.
- **SonarQube Analysis:** Validate analysis without errors.
- **Azure Web App:** Verify access via web app URL.
- **Release Pipeline:** Successful deployment without errors.

**Areas for Assistance:**
- Troubleshooting Docker build issues.
- Resolving authentication errors.
- Correcting SonarQube configurations.
- Debugging pipeline failures.

