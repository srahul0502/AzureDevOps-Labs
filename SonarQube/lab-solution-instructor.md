# Integrating SonarQube with Azure DevOps for Automated Code Analysis 

## Notes to Instructor

### Key Points to Verify

- Ensure that the student has successfully provisioned the Virtual Machine (VM) with the correct specifications and security settings.
- Verify that Docker has been installed and configured properly on the VM.
- Confirm that the SonarQube container is running and accessible via the browser.
- Check that the Azure DevOps service connection to SonarQube has been created correctly.
- Verify that the pipeline tasks for SonarQube analysis are configured in the correct sequence.
- Ensure the pipeline execution provides analysis results and displays a Quality Gate status.

### Common Challenges

- Students may face issues with Docker permissions or user group configurations.
- Network settings might block access to the SonarQube web interface.
- Incorrect configurations in the service connection may prevent integration with Azure DevOps.
- Pipeline task misplacement or incomplete configurations might result in failed or incomplete code analysis.

### Suggestions for Assistance

- Guide students on properly configuring Docker permissions and ensuring they re-login after adding the user to the Docker group.
- Assist with troubleshooting firewall and network rule settings to allow traffic on port 9000.
- Provide help in generating and using authentication tokens for the SonarQube service connection.
- Ensure that the sequence of pipeline tasks follows the correct order: **Prepare Analysis Configuration**, **Build Tasks**, **Run Code Analysis**, and **Publish Quality Gate Result**.

---

## Submission Checklist

- **Screenshot** showing the running SonarQube container.
- **Screenshot** confirming access to the SonarQube web interface.
- **Screenshot** of the Azure DevOps pipeline execution summary displaying SonarQube analysis results.
- **Confirmation** of the Quality Gate status.
- **A brief report** highlighting key learnings and challenges faced.

---

### Sample Report Summary

- **VM Setup:** Successfully provisioned an Ubuntu 22.04 LTS VM with t2.medium specifications and 20 GB storage.
- **Docker Installation:** Installed Docker and configured user permissions.
- **SonarQube Deployment:** Deployed SonarQube using the Docker image `sonarqube:lts-community`.
- **SonarQube Web Interface Access:** Accessible at `http://<VM_IP>:9000` with credentials updated upon first login.
- **Service Connection:** Created and configured a service connection in Azure DevOps for SonarQube integration.
- **Pipeline Configuration:**
    - Added **Prepare Analysis Configuration** task with the correct project key and server endpoint.
    - Successfully included **Run Code Analysis** and **Publish Quality Gate Result** tasks.
- **Pipeline Execution:** Analysis completed successfully, displaying Quality Gate results.

---

### Troubleshooting and Additional Notes

- **Docker Issues:** Resolved permission issues by adding the user to the Docker group and re-logging in.
- **Network Access:** Enabled port 9000 in firewall settings to allow external access.
- **Service Connection:** Generated and used an authentication token for secure communication between Azure DevOps and SonarQube.
- **Pipeline Task Configuration:** Ensured correct task sequence and configuration to achieve successful code analysis.
- **Challenges:** Faced initial issues with Docker permissions and firewall rules, which were resolved following best practices.

---


