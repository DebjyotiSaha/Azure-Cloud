### **📌 Deploying Resources with ARM Templates in Azure**  

Azure Resource Manager (ARM) is responsible for provisioning and managing **Azure resources** using declarative JSON templates. Here's a **step-by-step guide** on how to write and deploy ARM templates using **VS Code** and Azure CLI.  

---

## **1️⃣ Setting Up VS Code for ARM Templates**  
To write ARM templates efficiently, use **Visual Studio Code** with the **ARM Tools extension**:  
✅ Install **VS Code**  
✅ Install **ARM Tools** extension  

Once installed, create a **JSON file** (e.g., `storage-deploy.json`).  

Now, **type** `arm` and select the first suggestion. This will generate a basic template structure.  

---

## **2️⃣ Writing an ARM Template for Storage Account**  

### **📌 JSON Template (storage-deploy.json)**
```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2021-09-01",
      "name": "mystorageaccount123",
      "location": "eastus",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "StorageV2",
      "properties": {}
    }
  ]
}
```
🔹 **What this template does:**  
- Creates a **Storage Account**  
- Uses **Standard_LRS** redundancy  
- Specifies **StorageV2** type  

---

## **3️⃣ Deploying the ARM Template Using Azure CLI**  

### **Step 1: Create a Resource Group**
```sh
az group create \
  --name vscode \
  --location "Central US"
```
✅ This creates a **resource group** named `vscode`.  

### **Step 2: Deploy the Storage Account Using ARM Template**
```sh
az deployment group create \
  --resource-group vscode \
  --template-file storage-deploy.json
```
✅ This deploys the **storage account** inside the `vscode` resource group.  

---

## **4️⃣ Verifying the Deployment**  
Once deployed, check the Azure Portal:  
1️⃣ **Go to** *Resource Groups → vscode*  
2️⃣ **Check if** `mystorageaccount123` is created.  

---

## **5️⃣ Advantages of ARM Templates**  
🔹 **Automation** → No manual configuration, reduces human error.  
🔹 **Reusability** → The same template can be used multiple times.  
🔹 **Consistency** → Ensures all deployments follow the same structure.  
