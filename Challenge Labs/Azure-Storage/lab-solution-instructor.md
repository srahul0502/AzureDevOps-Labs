# Azure Storage: Create a Blob Storage and Connect via Storage Explorer

## Notes to Instructor

### Common Challenges and Tips

**Storage Account Configuration Issues:**

- Users may forget to enable secure access or configure redundancy properly.
- **Tip:** Ensure users select the correct redundancy option (e.g., LRS, GRS) and enable secure transfer.

**Access Level Misconfiguration:**

- Students might incorrectly set container access levels, exposing private data.
- **Tip:** Emphasize using private access levels unless public access is explicitly required.

**Storage Explorer Connection Errors:**

- Authentication issues may arise due to incorrect account keys or SAS tokens.
- **Tip:** Verify that users copy the complete connection string or generate valid SAS tokens.

## Submission Checklist

- **Screenshots:**
    - Storage account and container setup
    - File upload in the container
    - Successful connection in Storage Explorer
- Detailed report with verification steps and key observations

## Solution

### Step 1: Deploy a Storage Account

**Navigate to the Azure Portal:**

- Open [Azure Portal](https://portal.azure.com) and log in with your credentials.

**Create a Storage Account:**

1. Click **Create a resource > Storage > Storage account**.
2. Configure the following settings:
    - **Subscription:** Select your subscription.
    - **Resource Group:** Create a new one or select an existing group.
    - **Storage Account Name:** Provide a globally unique name.
    - **Region:** Select a nearby region.
    - **Performance:** Standard
    - **Redundancy:** Locally-redundant storage (LRS) or as per lab requirements
3. Click **Review + Create > Create**.

💡 **Instructor Tip:** Highlight the importance of choosing the right redundancy option for data durability.

**Verification:**

- Confirm the storage account appears in the Azure Portal under Storage accounts.

### Step 2: Configure Blob Storage Containers

**Access the Storage Account:**

- Navigate to the newly created storage account.
- Select **Containers** from the left menu.

**Create a Blob Container:**

1. Click **+ Container**.
2. Provide a name (e.g., `mycontainer`).
3. Set **Public Access Level** to **Private (no anonymous access)**.
4. Click **Create**.

**Verification:**

- Ensure the container is listed under the storage account.

💡 **Instructor Tip:** Emphasize the importance of private access for sensitive data.

### Step 3: Connect to Storage via Azure Storage Explorer

**Install Storage Explorer:**

- Download and install [Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/).

**Connect to Storage Account:**

1. Open Storage Explorer.
2. Click **Add an Account** or **Connect to Azure Storage**.
3. Choose one of the following methods:
    - **Subscription:** Sign in and select the storage account.
    - **Connection String:** Copy the connection string from the Azure Portal under Access keys.

**Verification:**

- Navigate to the connected storage account and confirm the visibility of the blob container.

💡 **Instructor Tip:** Demonstrate both subscription-based and connection string methods for connecting.

### Step 4: Data Operations Challenge

**Upload a File:**

1. Navigate to the blob container.
2. Click **Upload** and select a file (e.g., `datafile.txt`).
3. Click **Upload** to confirm.

**Download the File:**

1. Right-click the uploaded file and select **Download**.
2. Verify the file’s integrity by opening it.

**Modify Blob Properties:**

1. Right-click the blob and select **Properties**.
2. Change access tier (e.g., from Hot to Cool).
3. Add metadata (e.g., key: `description`, value: `sample file`).

**Verification:**

- Confirm the file upload, successful download, and property changes in Storage Explorer.

💡 **Instructor Tip:** Explain the cost implications of different blob access tiers.

### Sample Report Summary

**Verification Tips:**

- **Storage Account:** Ensure secure transfer is enabled.
- **Blob Container:** Validate private access level.
- **Storage Explorer:** Confirm successful connection and data operations.

**Common Errors:**

- Incorrect container access levels
- Connection string issues
- Metadata not saved properly

## Additional Notes

- Encourage troubleshooting and independent problem-solving.
- Highlight best practices for secure and efficient data storage in Azure.
