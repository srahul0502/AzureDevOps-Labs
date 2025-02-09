# Configuring Auto Scaling for Virtual Machines in Azure

## Lab Overview

In this guided lab, you will learn how to configure auto-scaling for Virtual Machines (VMs) in Azure. Auto-scaling enables the dynamic adjustment of VM resources based on demand, ensuring optimal performance and cost efficiency. By the end of this lab, you will have hands-on experience in setting up auto-scaling for VMs in Azure and understanding how to automate resource management.

## Pre-requisites

- An active Azure subscription with the necessary permissions to create resources.
- Basic understanding of Azure Virtual Machines and the Azure Portal.
- Familiarity with scaling concepts and cloud resource management.

## Learning Objectives

By the end of this lab, you will be able to:

- Understand the concept of auto-scaling and its benefits in Azure.
- Create and configure auto-scaling rules for virtual machines.
- Automatically scale VMs based on metrics such as CPU utilization or memory usage.
- Monitor and manage auto-scaling activities in Azure.

## Lab Description

This lab walks you through the process of setting up auto-scaling for Azure Virtual Machines. You will learn how to define auto-scaling rules, set thresholds, and automatically adjust the number of VM instances to maintain performance and cost efficiency.

## TASKS

### Task 1: Enable Auto-Scaling for a Virtual Machine

**Objective:** Enable auto-scaling for a Virtual Machine in Azure.

**Instructions:**

1. Navigate to the Azure Portal and search for Virtual Machines.
2. Select the desired Virtual Machine from the list.
3. On the VM Overview page, go to the Scaling section under Settings.
4. Click Enable auto-scaling and configure the following settings:
    - **Minimum Instances:** Set to 1 to handle light workloads.
    - **Maximum Instances:** Set to 5 to prevent over-scaling.
5. Click Save to apply the changes.

**Verification:**

- Ensure auto-scaling is enabled with the minimum and maximum instances settings displayed correctly on the scaling configuration page.

---

### Task 2: Define Auto-Scaling Rules Based on Metrics

**Objective:** Define scaling rules based on CPU utilization.

**Instructions:**

1. In the Auto-Scaling configuration, under Scaling Rules, click Add a rule.
2. Configure the Scaling Out Rule:
    - **Metric:** CPU Utilization.
    - **Operator:** Greater than.
    - **Threshold:** Set to 80% for scaling out.
    - **Action:** Increase the instance count by 1.
    - **Cool-down period:** Set to 5 minutes to avoid rapid scaling.
3. Configure the Scaling In Rule:
    - **Metric:** CPU Utilization.
    - **Operator:** Less than.
    - **Threshold:** Set to 30% for scaling in.
    - **Action:** Decrease the instance count by 1.
    - **Cool-down period:** Set to 5 minutes.
4. Click Save to apply the rules.

**Verification:**

- Confirm that both scaling rules (scaling out and scaling in) are listed in the scaling configuration, with the correct metrics, actions, and cool-down periods.

---

### Task 3: Monitor Auto-Scaling Activity

**Objective:** Monitor the performance and activity of auto-scaling for your virtual machine.

**Instructions:**

1. Navigate to your Virtual Machine in the Azure Portal.
2. Under the **Metrics section**, select **CPU Utilization** to monitor the performance of your VM.
3. Check the Scaling tab to view if scaling actions have been triggered based on the defined rules.
    - Look for changes in the instance count corresponding to CPU utilization thresholds.

**Verification:**

- Ensure that scaling activity reflects the changes in instance count as per the rules set (e.g., when CPU utilization exceeds 80%, the instance count should increase).

---

### Task 4: Test Auto-Scaling Behavior

**Objective:** Test the auto-scaling behavior by simulating increased or decreased load.

**Instructions:**

1. Simulate load on your VM using a stress testing tool like stress-ng or by running resource-intensive applications.
2. In the Azure Portal, monitor the CPU Utilization metric:
    - When the CPU usage exceeds 80%, confirm that the VM instances scale out (increase).
    - After reducing the load, ensure that the instances scale back down when CPU utilization falls below 30%.
3. Capture screenshots showing the scaling events and the number of instances before and after scaling.

**Verification:**

- Verify that the instance count changes correctly based on the CPU utilization.
- Confirm that the scaling actions (increasing/decreasing instances) happen smoothly, without any rapid scaling due to the cool-down period.

## Submission Guidelines

- Submit a screenshot of the Auto-Scaling Configuration showing the scaling rules and minimum/maximum instance settings.
- Include a brief explanation of how auto-scaling works in Azure and how you monitored the scaling activity.
- Upload the screenshot and description to the designated submission portal.

## Additional Resources

- [Azure Documentation: Virtual Machine Auto-Scaling](https://learn.microsoft.com/azure/virtual-machine-scale-sets/autoscale-overview)
- [Azure Monitoring and Metrics](https://learn.microsoft.com/azure/monitoring-and-metrics/)
