**Lab Title: Running Playwright Test Cases via Azure DevOps and Publishing the Report**

## Lab Overview
This lab provides a step-by-step guide to run Playwright test cases in Azure DevOps and publish test reports. You will learn how to set up a pipeline using the classic editor, install Node.js, configure test tasks, and publish results and artifacts.

## Pre-requisites
- An active Azure DevOps account
- A project in Azure DevOps
- Basic knowledge of Node.js and Playwright
- A Playwright project with a valid `package.json` file
- Appropriate access rights to create and manage pipelines in Azure DevOps

## Learning Objectives
By the end of this lab, you will be able to:
1. Clone a repository into Azure Repos.
2. Set up an Azure DevOps pipeline to execute Playwright tests.
3. Configure tasks to install dependencies and run tests.
4. Publish test results and reports as pipeline artifacts.

## Description
This lab walks you through creating an Azure DevOps pipeline using the classic editor. You will configure tasks to install Node.js, run Playwright tests, and publish test reports and artifacts. By the end of the lab, you will have a fully functional pipeline to automate Playwright test execution and report publication.

## TASKS

### Task 1: Clone the Repository to Azure Repos
#### Objective
Import your Playwright project into Azure Repos.

#### Instructions
1. Navigate to your Azure DevOps project.
2. Select **Repos** from the left menu.
3. Click on **Import Repository** if you want to import from an external source, or select **Clone Repository** to clone your local repository.
4. If importing, provide the URL of your existing repository and click **Import**.
5. If cloning, copy the clone URL, navigate to your terminal, and use the following command:
   ```bash
   git clone <repo-url>
   ```
6. Push your project to Azure Repos:
   ```bash
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

#### Verification
Ensure your project files are visible in Azure Repos.

---

### Task 2: Create a New Pipeline
#### Objective
Set up a new Azure DevOps pipeline using the classic editor.

#### Instructions
1. Navigate to your Azure DevOps project.
2. Click on **Pipelines** from the left menu.
3. Click on **New Pipeline**.
4. Select **Use the classic editor** and click **Continue**.
5. Select your source repository and click **Continue**.
6. Choose **Empty job** to start with a blank pipeline.

#### Verification
Ensure that a new pipeline template with a single empty job is created.

---

### Task 3: Install Node.js
#### Objective
Add a task to install Node.js as it is required for running Playwright.

#### Instructions
1. Click the **+** icon to add a new task.
2. Search for **Node.js tool installer** and add it to the pipeline.
3. Select the newly added task.
4. Set **Node.js version** to `16` (Playwright supports Node.js v14 and above).
5. Save the configuration.

#### Verification
Ensure the task appears in the pipeline with Node.js v16 selected.

---

### Task 4: Install Playwright and Dependencies
#### Objective
Install Playwright and its dependencies using a command-line task.

#### Instructions
1. Click the **+** icon to add another task.
2. Search for **Command Line** and add it.
3. Set **Display name** to `Install Playwright & Dependencies`.
4. Under **Script**, enter the following:
   ```bash
   npm install && npx playwright install
   ```
5. Click **Advanced**, then click the small information (i) icon to select the working directory for the task.
6. Save the configuration.

#### Verification
Ensure the command-line task appears with the correct script.

---

### Task 5: Configure NPM Task to Run Tests
#### Objective
Run Playwright tests by referring to the `package.json` file.

#### Instructions
1. Click the **+** icon to add another task.
2. Search for **npm** and add it.
3. Set **Display name** to `Run Playwright Tests`.
4. Under **Command**, select `custom`.
5. In **Command and arguments**, enter `run tests`.
6. Save the configuration.

#### Verification
Ensure the npm task is configured to run tests.

![alt text](<Screenshot 2025-02-09 092437.png>)

---

### Task 6: Publish Playwright Report
#### Objective
Publish Playwright reports as pipeline artifacts.

#### Instructions
1. Add a **Publish Pipeline Artifacts** task.
2. Configure it to point to the directory containing the Playwright report.
3. Save the configuration.

#### Verification
Ensure that the task appears and is correctly configured.



---

### Task 7: Publish Test Results
#### Objective
Publish test results for better visibility.

#### Instructions
1. Add a **Publish Test Results** task.
2. Configure it to point to the Playwright test results file.
3. Save the configuration.

![alt text](<Screenshot 2025-02-09 092539.png>)

#### Verification
Ensure that the task appears and is configured correctly.

---

### Task 8: Final Execution
#### Objective
Run the complete pipeline and verify results.

#### Instructions
1. Click **Run pipeline**.
2. Monitor the execution.
3. Verify that artifacts and test results are published.

![alt text](<Screenshot 2025-02-09 092745.png>)

#### Verification
Ensure that test results and artifacts are visible in the pipeline.

## Submission Guidelines
1. Take screenshots of each configured task.
2. Capture the final pipeline execution result.
3. Submit a document containing the screenshots and a brief description of the pipeline configuration.

## Additional Resources
- [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/?view=azure-devops)
- [Playwright Documentation](https://playwright.dev/docs/intro)
- [Node.js Official Site](https://nodejs.org/)

