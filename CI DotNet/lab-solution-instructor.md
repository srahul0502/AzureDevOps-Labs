# Continuous Integration for a .NET Application Covering Build, Test, Scan, and Publishing Artifact via Azure DevOps

## Notes to Instructor

### Key Points to Verify

- **Service Connections:**
  - Ensure the **SonarQube** service connection is correctly configured with the appropriate server URL and authentication token.

- **Pipeline Configuration:**
  - Verify that the Classic Pipeline includes all specified tasks: NuGet installation, solution build, unit testing, SonarQube preparation and analysis, and artifact publishing.
  - Check that each task is configured with the correct parameters and references the appropriate service connections.

- **Artifact Generation:**
  - Ensure the pipeline successfully generates and archives the build artifacts for the .NET application.

- **SonarQube Analysis:**
  - Confirm that the code analysis results are available in the SonarQube project dashboard and reflect the latest pipeline run.

### Common Challenges

- **Service Connection Issues:**
  - Students may encounter difficulties in setting up service connections due to permission restrictions or incorrect configurations.

- **Pipeline Task Failures:**
  - Misconfigurations in task parameters, such as incorrect paths or missing variables, can lead to pipeline failures.

- **Artifact Publishing Errors:**
  - Incorrect source or target paths in the file copy task may result in missing or improperly published artifacts.

- **SonarQube Integration Problems:**
  - Issues with the SonarQube server URL or authentication token can prevent successful code analysis.

### Suggestions for Assistance

- **Service Connections:**
  - Guide students through the process of setting up service connections, ensuring they have the necessary permissions and correct configurations.

- **Pipeline Configuration:**
  - Assist in verifying task parameters, emphasizing the importance of correct paths and variable usage.

- **Artifact Verification:**
  - Encourage students to check the artifact directories to confirm the presence of the expected files.

- **SonarQube Troubleshooting:**
  - Help students validate their SonarQube configurations, including server accessibility and token validity.

---

## Submission Checklist

- **Screenshot** of the **SonarQube Service Connection** configuration.
- **Screenshot** of the **Pipeline Configuration**, displaying all tasks.
- **Screenshot** of the **Pipeline Run Summary**, indicating a successful execution.
- **Screenshot** of the **Published Artifacts**, showing the build output.
- **Screenshot** of the **SonarQube Project Dashboard**, displaying the analysis results.
- **A brief report** summarizing the configurations and validations performed.

### Sample Report Summary

- **Service Connections:**
  - Established a SonarQube service connection named `Sonar` using the provided server URL and authentication token.

- **Pipeline Configuration:**
  - Set up a Classic Pipeline with the following tasks:
    - **NuGet Tool Installer:** Installed the latest version of NuGet.
    - **Solution Build:** Configured to build the solution and create deployment artifacts.
    - **Unit Tests:** Configured to run tests from the specified project.
    - **Prepare SonarQube Analysis:** Connected to the SonarQube server and prepared for analysis.
    - **Run Code Analysis:** Performed static code analysis using SonarQube.
    - **Publish Build Artifacts:** Published the build outputs.

- **Artifact Verification:**
  - Verified the presence of build artifacts in the pipeline run.

- **SonarQube Analysis:**
  - Successfully accessed the SonarQube project dashboard and validated the analysis results.

## Additional Recommendations

1. **Automate Unit Testing with CI:**
   - Ensure all unit tests run on every commit to maintain software quality.

2. **Pipeline Status Notifications:**
   - Configure email or Teams notifications to inform stakeholders of pipeline status.

3. **Version Control Best Practices:**
   - Encourage the use of feature branches and pull request validations.

4. **Security Measures:**
   - Implement role-based access control for pipelines and service connections.

5. **Regular SonarQube Scans:**
   - Schedule periodic scans and reviews for improved code quality and security.

