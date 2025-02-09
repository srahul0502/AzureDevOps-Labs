# Running Playwright Test Cases via Azure DevOps and Publishing the Report

## Notes to Instructor

### Key Points to Verify

- Ensure that the student successfully cloned their Playwright project into Azure Repos.
- Confirm the creation of the pipeline using the classic editor and proper task configurations.
- Verify the correct installation of Node.js and Playwright.
- Check the configuration for running tests and publishing reports.
- Ensure test results and Playwright reports are visible as pipeline artifacts.

### Common Challenges

- **Repository Cloning:** Students may encounter issues when pushing their local repository to Azure Repos.
  - Solution: Verify that the repository URL and authentication details are correctly configured.
- **Node.js Installation:** Incorrect Node.js version selection might cause compatibility issues.
  - Solution: Ensure Node.js version `16` or higher is used.
- **Playwright Installation:** Errors may occur during installation if dependencies are not correctly resolved.
  - Solution: Guide students to troubleshoot by reviewing error logs and ensuring the package.json file is valid.
- **Publishing Reports:** Students may face directory path issues when publishing artifacts.
  - Solution: Verify the correct directory paths and report locations.

### Suggestions for Assistance

- Assist students in troubleshooting issues during repository cloning by verifying SSH keys or access permissions.
- Help debug npm installation errors by reviewing package.json and terminal logs.
- Provide guidance on properly setting paths for test result artifacts.
- Recommend thorough testing by rerunning the pipeline after initial configuration.

---

## Submission Checklist

- **Screenshot** showing the repository successfully cloned into Azure Repos.
- **Screenshot** of each configured pipeline task.
- **Screenshot** showing the successful pipeline execution.
- **Screenshot** of test results and artifacts published.
- **A brief report** summarizing the pipeline configuration and execution.

### Sample Report Summary

- **Repository Cloning:** Successfully cloned the Playwright project into Azure Repos and confirmed visibility of project files.
- **Pipeline Creation:** Created a new pipeline using the classic editor with an empty job template.
- **Node.js Installation:** Added and configured the Node.js tool installer task to use version `16`.
- **Playwright Installation:** Successfully installed Playwright and its dependencies using a command-line task.
- **Test Execution:** Configured the npm task to execute Playwright tests, and tests ran successfully.
- **Report Publication:** Published Playwright reports and test results as pipeline artifacts.
- **Testing:** Verified the availability of test reports and results in the pipeline.

### Troubleshooting and Additional Notes

- **Repository Push Errors:** Ensure the correct use of `git push origin main` and appropriate commit messages.
- **Node.js Errors:** Double-check the version used and Node.js tool installer configuration.
- **Test Execution Errors:** Verify that the `package.json` file contains the correct test scripts.
- **Artifact Issues:** Ensure directory paths for artifacts and test results are correctly configured in tasks.

---

## Additional Resources

- [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/?view=azure-devops)  
- [Playwright Documentation](https://playwright.dev/docs/intro)  
- [Node.js Official Site](https://nodejs.org/)

