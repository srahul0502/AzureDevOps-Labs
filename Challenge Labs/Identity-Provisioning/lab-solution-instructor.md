# Solution: Identity Provisioning in Azure Challenge Lab

## Notes to Instructor

### Common Challenges and Tips

1. **User Creation and Group Assignment Issues:**
    - Students may encounter issues creating users or adding them to the security group.
    - **Tip:** Ensure the users are created successfully in Azure AD and that they appear in the security group.

2. **Role Assignment and Permissions:**
    - Students might forget to assign the correct role or misconfigure permissions for the group.
    - **Tip:** Double-check the role assignments in the Azure Portal under "Access control (IAM)" for the resource group.

3. **MFA Configuration Challenges:**
    - Some students might struggle with enabling MFA for all users.
    - **Tip:** Walk them through the process of enabling MFA using the Azure portal or PowerShell.

4. **Conditional Access Policy Configuration:**
    - Students may have trouble setting up the conditional access policy or testing it from different locations.
    - **Tip:** Guide them through configuring a basic MFA policy and testing it using different network locations.

## Submission Checklist

- Screenshots:
    - User and group creation in Azure AD
    - Role assignments for the security group
    - Multi-Factor Authentication (MFA) status
    - Conditional Access policy configuration
- Report summarizing the steps taken, including any verification and troubleshooting.

### Sample Report Summary

**Verification Tips:**

- **User Creation:** Ensure users are listed in the Azure AD users section.
- **Role Assignment:** Confirm that the users in the security group have the correct permissions on the specified resource group.
- **MFA Setup:** Verify that MFA is enabled and that users are prompted for additional verification when signing in.
- **Conditional Access Testing:** Use different IP locations (e.g., internal network vs. external) to test the conditional access policy and confirm MFA is triggered.

**Areas for Assistance:**

- Role assignment issues: Ensure correct roles are applied to the group.
- MFA enforcement: Make sure MFA is fully enforced by checking the sign-in logs.
- Conditional Access policy configuration: Help with testing policies from different locations.

## Solution:

### Step 1: Create Users and Groups in Azure AD

1. **Go to Azure AD** in the Azure Portal.
2. **Create Three Users:**
    - Navigate to Azure AD > Users > New User.
    - Create three users with relevant names, email addresses, and usernames.
3. **Create a Security Group:**
    - Go to Azure AD > Groups > New Group.
    - Create a security group named `IdentityLabGroup` and select "Security" as the group type.
4. **Add Users to the Group:**
    - Go to the created group, and add the three users to it by clicking on the “Members” section and selecting the users.

    💡 Instructor Tip: Ensure the users are added correctly and listed under the group’s membership.

### Step 2: Assign Roles to the Security Group

1. **Navigate to the Resource Group:**
    - Go to the Azure Portal > Resource Groups and select the specific resource group where the permissions will be assigned.
2. **Assign the Contributor Role to the Security Group:**
    - In the resource group, go to “Access control (IAM)” and click on “Add role assignment.”
    - Assign the **Contributor** role to the `IdentityLabGroup`.
    - Save the role assignment.

    💡 Instructor Tip: Make sure the role is assigned to the group, not individual users.

### Step 3: Enable Multi-Factor Authentication (MFA)

1. **Go to Azure AD > Security > Multi-Factor Authentication.**
2. **Enable MFA for All Users:**
    - Under the MFA section, select the option to "Enable" MFA for all users or select the specific users for whom MFA needs to be enforced.
    - Users will need to authenticate using MFA when signing in.

    💡 Instructor Tip: Verify that MFA is enabled by checking the status in the MFA section.

### Step 4: Configure Conditional Access Policies

1. **Navigate to Azure AD > Security > Conditional Access.**
2. **Create a New Policy:**
    - Click on "New Policy" and name it `Require MFA for Untrusted Locations`.
    - Under "Assignments," configure the policy to apply to all users.
    - Set the conditions to require MFA when accessing resources from locations outside the corporate network or from untrusted IPs.
3. **Enable the Policy:**
    - Under "Access Controls," select **Grant** > **Require multi-factor authentication**.
    - Save and enable the policy.

    💡 Instructor Tip: Test the conditional access policy by accessing resources from a trusted vs. untrusted location (e.g., internal vs. external network).

### Step 5: Verify the Configuration

1. **Check the User and Group Configuration:**
    - Confirm that the users are successfully created and added to the group in Azure AD.
2. **Validate Role Assignments:**
    - Ensure that the security group has the correct Contributor role assigned to the resource group.
3. **Test MFA:**
    - Try signing in as one of the users and confirm that MFA is prompted.
4. **Test Conditional Access Policy:**
    - Access resources from an untrusted location (such as an external network) to ensure that the MFA is triggered by the policy.

## Submission Checklist

- **Screenshots of:**
    - User and group creation
    - Role assignments in the resource group
    - MFA status in the Azure AD portal
    - Conditional access policy configuration
- **Report summarizing:**
    - Approach and tasks completed
    - Challenges faced and solutions implemented

### Sample Report Summary

**Verification Tips:**

- Ensure users are correctly listed in Azure AD and added to the group.
- Confirm role assignments by checking access control settings for the resource group.
- MFA should be enforced, and the user should be prompted for additional verification upon sign-in.
- Test the conditional access policy by attempting to sign in from different network locations.

**Common Errors:**

- Incorrect role assignment to the security group
- MFA not enabled for all users
- Conditional access policy not applied correctly

## Additional Notes

- Troubleshoot independently when students face issues and provide guidance as needed.
- Emphasize the importance of secure identity management in Azure and how best practices such as MFA and conditional access enhance security.
