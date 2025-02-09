# Protecting Azure Resources: Creating and Testing Resource Locks


## Lab Overview  
In this lab, you will apply their knowledge of Azure resource management by creating a resource lock to protect an Azure resource from accidental changes or deletion. This is a **challenge lab**, where only task objectives and minimal instructions are provided to encourage self-learning.

---

## Pre-requisites  
- Azure subscription access  
- Basic understanding of resource groups and resources in Azure  
- Familiarity with the Azure Portal and Azure CLI  

---

## Learning Objective  
- Implement resource locks in Azure to prevent unintended changes or deletion of resources  

---

## Description  
Participants will be required to create and test resource locks for Azure resources such as Virtual Machines or Storage Accounts. They need to ensure that resources are protected from accidental deletions or updates, following best practices.

---

## Scenario Context  
**Use Case:** Imagine you are managing a critical production Virtual Machine (VM) hosting the primary application for an e-commerce website. If this VM is accidentally deleted or modified, it could result in significant downtime, revenue loss, and customer dissatisfaction. Therefore, it's essential to protect this VM by applying a resource lock.

Your task is to safeguard the critical production resource from unintended changes using Azure's locking mechanism.

---

## TASKS  

### Task 1: Select a Target Resource  
**Objective:** Choose an existing resource or create a new resource for this lab (e.g., Virtual Machine, Storage Account, or Web App).  
**Instructions:**  
- Ensure the selected resource belongs to an accessible resource group.  

**Verification:**  
- Verify the resource status in the resource group.  

---

### Task 2: Create a Resource Lock  
**Objective:** Apply a resource lock to prevent resource deletion.  
**Instructions:**  
- Choose the correct lock level (`CanNotDelete` or `ReadOnly`).  
- Use either the Azure Portal or CLI to set the lock.

**Verification:**  
- Attempt to delete the resource after applying the lock and confirm that the deletion is blocked.  

---

### Task 3: Test the Resource Lock  
**Objective:** Confirm that changes and deletions are appropriately restricted.  
**Instructions:**  
- Test the impact of the lock by attempting to modify and delete the resource.  

**Verification:**  
- Note the error message shown due to the resource lock.  

---

### Task 4: Remove the Resource Lock (Optional)  
**Objective:** Remove the resource lock to allow normal operations.  
**Instructions:**  
- Use the Azure Portal or CLI to delete the lock.  

**Verification:**  
- Verify the resource is now modifiable and deletable.  

---

## Submission Guidelines  
Provide a document containing:  
1. Name and type of resource used.  
2. CLI or screenshot evidence of lock creation.  
3. Verification results when attempting to delete or modify the locked resource.  
4. Reflection on how resource locks can be useful in a production environment.

---

## Additional Resources  
- [Azure Resource Locks Documentation](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/lock-resources)  
- [Azure CLI Documentation](https://learn.microsoft.com/en-us/cli/azure/)  

---

