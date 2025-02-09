# Deploy and Configure Azure Traffic Manager - Solution

## Notes to Instructor

### Common Challenges

- **DNS Propagation Delays:** DNS changes may take several minutes to propagate, so students may not see immediate results when testing traffic routing after configuration.
- **Endpoint Configuration:** Students might face issues with selecting the correct endpoint type or misconfiguring priority settings.
- **Traffic Routing Testing:** Ensure that students properly simulate failure by stopping one of the web apps, as this directly impacts their testing results.

### Suggestions for Assistance

- Guide students in troubleshooting DNS propagation delays by explaining that it might take up to 5 minutes for changes to reflect.
- If students face difficulty in configuring endpoints, assist them in verifying that both web apps are correctly deployed and in a Running state before adding them to Traffic Manager.
- Help students monitor the Traffic Manager profile and DNS traffic by verifying both the DNS Name and routing status.

---

## Submission Checklist

- **Screenshots** of both web apps running in the `TrafficManagerLabRG or labs` resource group.
- **Screenshot** of the Traffic Manager profile with both endpoints configured (showing priority settings).
- **Screenshot** of traffic routing to the second web app after stopping the first one.
- **A brief report** summarizing the traffic routing behavior and any issues encountered.

### Sample Report Summary

- **Verification Tips:**
    - Confirm that both web apps are running and listed in the `TrafficManagerLabRG or labs` resource group.
    - Ensure that the Traffic Manager profile has both web app endpoints configured with appropriate priority settings.
    - Verify that traffic is routed to the correct web app based on DNS resolution after simulating an endpoint failure.

- **Areas for Assistance:**
    - Help students who encounter issues with DNS propagation by explaining the expected wait time for changes to take effect.
    - Assist in understanding the impact of scaling settings in Traffic Manager, especially for performance-based routing.
    - Provide guidance on troubleshooting if traffic routing does not behave as expected.

---

## Solution

### Task 1: Create Web App Endpoints

**Steps:**

1. **Log in to the Azure Portal:**
    - Open a web browser and navigate to Azure Portal.
    - Sign in with your Azure account credentials.

2. **Create the First Web App:**
    - In the left-hand menu, click **Create a resource**.
    - Search for **Web App** and select it from the search results.
    - Click **Create** to launch the web app creation wizard.
    - Fill in the following details:
        - **Subscription:** Select your subscription.
        - **Resource Group:** Click **Create new** and name it `TrafficManagerLabRG or labs`.
        - **Name:** Enter a globally unique name, e.g., `TrafficManagerLabRG`.
        - **Publish:** Select **Code**.
        - **Runtime Stack:** Choose `.NET 6 (LTS)`.
        - **Operating System:** Select **Windows**.
        - **Region:** Select **East US**.
    - Click **Next: Monitoring** and disable Application Insights.
    - Click **Review + Create**, and then click **Create**.

3. **Create the Second Web App:**
    - Repeat the above process but use the following details:
        - **Resource Group:** Select `TrafficManagerLabRG or labs`.
        - **Name:** Enter a unique name, e.g., `TrafficManagerLabRG2`.
        - **Region:** Select **West US**.

4. **Verify Web App Deployments:**
    - Navigate to **Resource Groups > TrafficManagerLabRG**.
    - Ensure both `TrafficManagerLabRG` and `TrafficManagerLabRG2` are listed and in the **Running** state.

**Verification:**

- Confirm that both web apps are running by checking their status in the portal.

### Task 2: Create an Azure Traffic Manager Profile

**Steps:**

1. **Navigate to Traffic Manager Profiles:**
    - In the Azure Portal, search for **Traffic Manager Profiles**.
    - Select **Traffic Manager Profiles** from the search results.

2. **Create a Traffic Manager Profile:**
    - Click **Create**.
    - Configure the profile with the following details:
        - **Subscription:** Select your subscription.
        - **Resource Group:** Select `TrafficManagerLabRG or labs`.
        - **Name:** Enter a unique name, e.g., `TrafficManagerLabProfile`.
        - **Routing Method:** Select **Priority**.
        - **Resource Location:** Select **Global**.
    - Click **Review + Create**, then click **Create**.

**Verification:**

- Ensure the Traffic Manager profile is successfully created and accessible.

### Task 3: Add Endpoints to the Traffic Manager Profile

**Steps:**

1. **Open the Traffic Manager Profile:**
    - Navigate to the newly created `TrafficManagerLabProfile`.

2. **Add the First Endpoint:**
    - Under Settings, click **Endpoints**.
    - Click **Add** and configure the first endpoint as follows:
        - **Type:** Select **Azure Endpoint**.
        - **Name:** `WebAppEndpint1`
        - **Target Resource Type:** Select **App Service**.
        - **Target Resource:** Select `TrafficManagerLabRG`.
        - **Priority:** Set to `1`.
    - Click **OK**.

3. **Add the Second Endpoint:**
    - Click **Add** again.
    - Configure the second endpoint as follows:
        - **Type:** Select **Azure Endpoint**.
        - **Name:** `WebAppEndpint2`
        - **Target Resource Type:** Select **App Service**.
        - **Target Resource:** Select `TrafficManagerLabRG2`.
        - **Priority:** Set to `2`.
    - Click **OK**.

**Verification:**

- Verify that both endpoints are listed with the correct priority settings.

### Task 4: Test Traffic Routing

**Steps:**

1. **Access the Traffic Manager DNS:**
    - In the Traffic Manager profile overview, copy the DNS Name.
    - Open a web browser and paste the DNS name.
    - Verify that the web app hosted in `TrafficManagerLabRG` is displayed.

2. **Simulate Endpoint Failure:**
    - Navigate to `TrafficManagerLabRG` in the Azure Portal.
    - Click **Stop** to stop the web app.
    - Wait for a few minutes (DNS propagation).
    - Refresh the DNS URL in your browser.
    - Verify that traffic is now routed to `TrafficManagerLabRG2`.

3. **Restart the First Web App:**
    - Navigate back to `TrafficManagerLabRG`.
    - Click **Start** to restart the web app.

**Verification:**

- Verify that traffic was rerouted to the second web app after stopping the first one.

### Task 5: Change Routing Method

**Steps:**

1. **Modify Routing Method:**
    - Navigate to the Traffic Manager profile.
    - Under Configuration, change the Routing Method to **Performance**.
    - Click **Save**.

2. **Test the New Routing Method:**
    - Access the Traffic Manager DNS URL.
    - Verify that traffic is routed to the endpoint with the best performance based on your location.

**Verification:**

- Ensure that the DNS URL correctly routes traffic based on the new routing method.

## Additional Notes

- Encourage students to experiment with different routing methods (e.g., Geographic, Weighted).
- Discuss how Traffic Manager can be used to enhance application performance and availability across regions.
- Ensure students understand the implications of DNS propagation when testing traffic routing changes.
