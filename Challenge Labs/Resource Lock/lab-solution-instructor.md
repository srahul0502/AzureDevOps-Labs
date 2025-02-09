# Protecting Azure Resources: Creating and Testing Resource Locks

## Notes to Instructor

### Common Challenges and Tips

1. **Resource Selection Issues:**
    - Participants may struggle to identify suitable resources for locking.
    - **Tip:** Suggest using Virtual Machines or Storage Accounts for this exercise, as these are common examples of critical resources.

2. **Lock Level Confusion:**
    - Participants might be unsure about selecting between "CanNotDelete" and "ReadOnly" lock levels.
    - **Tip:** Explain that "CanNotDelete" prevents accidental deletions, while "ReadOnly" restricts both deletions and updates.

3. **Verification Steps:**
    - Participants might face issues when testing the lock by attempting resource deletions.
    - **Tip:** Ensure participants attempt both deletions and updates to verify that the locks are applied correctly.

4. **Removing Resource Locks:**
    - Participants might forget how to remove the locks after testing.
    - **Tip:** Guide them to navigate back to the resource's lock settings in the Azure Portal or use the CLI.

## Submission Checklist

- **Resource Information:**
    - Name and type of resource used.
- **Evidence:**
    - CLI commands or screenshots showing the creation of resource locks.
    - Verification results showing failure to modify or delete the locked resource.
- **Reflection:**
    - A brief write-up on the significance of resource locks in production environments.

## Solution:

### Step 1: Select a Target Resource

1. Go to the **Azure Portal**.
2. Select an existing resource or create a new resource (e.g., Virtual Machine or Storage Account).
    - **Verification:** Confirm that the resource is in a resource group and accessible.

   💡 **Instructor Tip:** Emphasize the importance of choosing a critical resource that mimics real-world production environments.

### Step 2: Create a Resource Lock

1. Navigate to the selected resource in the Azure Portal.
2. Go to **Settings > Locks** and click **Add**.
3. Enter the following details:
    - **Name:** Provide a descriptive name for the lock.
    - **Lock Type:** Choose between "CanNotDelete" or "ReadOnly" based on requirements.
    - **Notes:** Optionally add notes to explain the lock purpose.
4. Click **OK** to apply the lock.

Alternatively, use the Azure CLI:

```bash
az lock create --name "ResourceLock" --lock-type CanNotDelete --resource-group <ResourceGroupName> --resource-name <ResourceName> --resource-type <ResourceType>
```

   💡 **Instructor Tip:** Ensure participants understand when to choose "CanNotDelete" over "ReadOnly." The latter is more restrictive and suitable for highly sensitive resources.

### Step 3: Test the Resource Lock

1. Attempt to delete or modify the locked resource in the Azure Portal.
2. Note the error message displayed due to the resource lock.

**CLI Verification:**

```bash
az resource delete --name <ResourceName> --resource-group <ResourceGroupName> --resource-type <ResourceType>
```

   💡 **Instructor Tip:** Encourage participants to test both update and deletion scenarios to validate the effectiveness of the lock.

### Step 4: Remove the Resource Lock (Optional)

1. Navigate to **Settings > Locks** for the selected resource.
2. Select the lock and click **Delete**.

**CLI Command:**

```bash
az lock delete --name "ResourceLock" --resource-group <ResourceGroupName> --resource-name <ResourceName> --resource-type <ResourceType>
```

3. Verify that the resource is now modifiable and deletable.

   💡 **Instructor Tip:** Explain why removing locks might be necessary in certain operational scenarios, such as maintenance or upgrades.

## Sample Report Summary

**Verification Tips:**

- **Resource Selection:** Ensure the resource is critical to mimic production scenarios.
- **Lock Testing:** Confirm that both update and delete attempts are restricted.
- **Error Message:** Document the specific error messages received when attempting restricted operations.

**Common Errors:**

- Incorrect resource types selected for testing.
- Misconfigured lock levels.
- CLI syntax errors.

**Areas for Assistance:**

- Resource lock application and verification.
- Understanding lock level implications.
- Troubleshooting CLI command issues.

## Additional Notes

- Highlight best practices for protecting critical resources.
- Encourage participants to reflect on the significance of resource locks in preventing accidental deletions or changes.
- Reinforce the importance of testing and documentation in real-world scenarios.

