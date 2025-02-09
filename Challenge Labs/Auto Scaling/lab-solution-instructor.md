# Configuring Auto-Scaling for Virtual Machines using VMSS in Azure

## Notes to Instructor

### Common Challenges and Tips

1. **Scaling Rule Misconfigurations:**
    - Students may overlook the correct configuration of scaling rules, which could lead to VMs not scaling out or in as expected.
    - **Tip:** Verify that the scaling rules are correctly set with appropriate CPU utilization thresholds (80% for scaling out, 30% for scaling in).

2. **Cooldown Periods:**
    - Students might not configure the cooldown periods appropriately, which could cause scaling actions to trigger too quickly or too slowly.
    - **Tip:** Ensure that the cooldown period is set to 5 minutes for both scaling in and scaling out actions.

3. **Simulation of Load:**
    - Students may not effectively simulate load or monitor CPU utilization to trigger scaling actions.
    - **Tip:** Use stress-testing tools like `stress-ng` to generate load and ensure scaling actions occur when CPU utilization exceeds the defined threshold.

## Submission Checklist

- Architecture diagram of VMSS configuration, scaling rules, and instance count.
- **Screenshots:**
    - Auto-scaling rules configured in the VMSS.
    - CPU utilization metrics showing scaling actions.
    - Azure Monitor metrics showing scaling activity and resource utilization.
- Brief report explaining the configuration steps, load testing, and monitoring process.

### Sample Report Summary

**Verification Tips:**

- **Scaling Rules:** Ensure scaling actions are configured based on the CPU utilization thresholds.
- **Cooldown Period:** Verify that the cooldown period for scaling actions is set to 5 minutes.
- **Load Testing:** Confirm that scaling out occurs when CPU utilization exceeds 80%, and scaling in occurs when CPU utilization drops below 30%.

**Areas for Assistance:**

- Misconfigured scaling rules.
- Incorrect cooldown period.
- Issues with load testing tools or monitoring metrics.

## Solution:

### Step 1: Create a Virtual Machine Scale Set (VMSS)

1. Navigate to the Azure Portal > **Virtual Machine Scale Sets** > **Add**.
    - **Name:** VMSS-ScaleSet
    - **Region:** Select your desired region.
    - **Image:** Choose an Ubuntu 20.04 LTS image or Windows image.
    - **Authentication Type:** SSH or Password, based on preference.
    - **Instance Count:** Set the initial count to 2 (can be changed later).
    - **Enable Auto-Scaling**: Ensure auto-scaling is enabled during creation.
    - Click **Review + Create** > **Create**.

    💡 Instructor Tip: Explain the importance of selecting the right image and authentication method for VMSS.

### Step 2: Configure Auto-Scaling Rules for VMSS

1. Go to your **VMSS** resource.
2. Under the **Scaling** section, click **Add a scaling rule**.
3. Configure the **Scaling Out Rule**:
    - **Metric:** CPU Utilization.
    - **Operator:** Greater than.
    - **Threshold:** Set to 80% for scaling out.
    - **Action:** Increase instance count by 1.
    - **Cooldown period:** 5 minutes.
4. Configure the **Scaling In Rule**:
    - **Metric:** CPU Utilization.
    - **Operator:** Less than.
    - **Threshold:** Set to 30% for scaling in.
    - **Action:** Decrease instance count by 1.
    - **Cooldown period:** 5 minutes.
5. Click **Save** to apply the rules.

    💡 Instructor Tip: Emphasize the role of CPU utilization in dynamic scaling. Discuss how the cooldown period prevents over-scaling.

### Step 3: Monitor Auto-Scaling Activity

1. Navigate to the **Metrics** section of your VMSS.
2. Select **CPU Utilization** to monitor the performance of VM instances.
3. Go to the **Scaling** section to view scaling actions triggered by CPU utilization.

    💡 Instructor Tip: Discuss the importance of monitoring scaling actions to validate that the system is responding to the load effectively.

### Step 4: Test Auto-Scaling Behavior and Performance

1. Use a tool like **stress-ng** to simulate load on your VM instances.
    ```bash
    stress-ng --cpu 4 --timeout 10m
    ```
2. Monitor **CPU Utilization** in Azure Portal to confirm scaling out occurs when CPU utilization exceeds 80%.
3. After reducing the load, verify that scaling in occurs when CPU utilization falls below 30%.

    💡 Instructor Tip: Assist students with interpreting scaling events and verifying CPU usage during load testing.

### Optional Task: Configure Alerts for Auto-Scaling Events

1. In the **Azure Portal**, go to your **VMSS** and navigate to the **Alerts** section.
2. Create an alert for **CPU Utilization** when it exceeds a threshold (e.g., 80%).
3. Set up an alert for scaling events to notify you when the VMSS scales out or in.

    💡 Instructor Tip: Alerts provide an extra layer of monitoring and can help troubleshoot scaling behaviors.

## Submission Checklist

- Architecture diagram of the VMSS setup and scaling rules.
- **Screenshots of:**
    - Auto-scaling rules and configuration.
    - CPU Utilization metrics and scaling actions.
    - Alert configurations (optional).
- A brief report describing:
    - Configuration steps for VMSS and scaling rules.
    - Load testing methodology and results.
    - Monitoring and alerting setup.

### Sample Report Summary

**Verification Tips:**

- Ensure scaling actions are triggered correctly based on CPU utilization thresholds.
- Verify that scaling actions respect the defined cooldown periods.
- Use tools like `stress-ng` to simulate load and verify scaling behavior.

**Common Errors:**

- Incorrect scaling rule configuration (e.g., wrong metric or threshold).
- Cooldown periods set too short or too long.
- Load not generated sufficiently to trigger scaling actions.

## Additional Notes

- Encourage students to test with different instance counts and load conditions.
- Remind students to verify that all metrics and alerts are properly configured to avoid missed scaling events.
