# Continuous Integration for a Java Application Covering Build, Test, Scan, and Publishing Artifact via Azure DevOps (Classic Pipeline) - Solution

## Notes to Instructor

### Key Points to Verify

- **Service Connections:**
  - Ensure the **Azure Resource Manager (ARM)** service connection is correctly configured with the appropriate subscription and resource group.
  - Confirm the **SonarQube** service connection is established using the correct server URL and authentication token.

- **Pipeline Configuration:**
  - Verify that the Classic Pipeline includes all specified tasks: Maven build, file copying, artifact publishing, SonarQube preparation and analysis, and dependency checking.
  - Check that each task is configured with the correct parameters and references the appropriate service connections.

- **Artifact Generation:**
  - Ensure the pipeline successfully generates two artifacts:
    - The Java application JAR file.
    - The dependency check report in HTML format.

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

- **Screenshot** of the **ARM Service Connection** configuration.
- **Screenshot** of the **SonarQube Service Connection** configuration.
- **Screenshot** of the **Pipeline Configuration**, displaying all tasks.
- **Screenshot** of the **Pipeline Run Summary**, indicating a successful execution.
- **Screenshot** of the **Published Artifacts**, showing both the Java application and dependency check report.
- **Screenshot** of the **SonarQube Project Dashboard**, displaying the analysis results.
- **A brief report** summarizing the configurations and validations performed.

### Sample Report Summary

- **Service Connections:**
  - Created an ARM service connection named `ARM` linked to the appropriate subscription and resource group.
  - Established a SonarQube service connection named `Sonar` using the provided server URL and authentication token.

- **Pipeline Configuration:**
  - Set up a Classic Pipeline with the following tasks:
    - **Maven Build:** Configured to package the application with tests skipped.
    - **Copy Files:** Set to copy the generated JAR files to the artifact staging directory.
    - **Publish Build Artifacts:** Published the JAR files as the `drop` artifact.
    - **SonarQube Preparation:** Prepared the analysis with the project key `shopping` and project name `EKart`.
    - **SonarQube Analysis:** Executed the code analysis.
    - **Dependency Check:** Performed a dependency check on the project and uploaded the SARIF report.

- **Artifact Generation:**
  - Verified the generation of two artifacts:
    - The Java application JAR file.
    - The dependency check report in HTML format.

- **SonarQube Analysis:**
  - Confirmed that the code analysis results are available in the SonarQube project dashboard, reflecting the latest pipeline run.

### Troubleshooting and Additional Notes

- **Service Connection Validation:**
  - Ensured that both the ARM and SonarQube service connections were successfully verified during creation.

- **Pipeline Execution:**
  - Monitored the pipeline run to identify and resolve any task failures promptly.

- **Artifact Verification:**
  - Checked the artifact directories post-pipeline execution to confirm the presence of the expected files.

- **SonarQube Access:**
  - Verified access to the SonarQube server and the availability of the project dashboard for analysis results.

---

## Additional Resources

- [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/)
- [Maven Documentation](https://maven.apache.org/)
- [SonarQube Documentation](https://www.sonarqube.org/)
