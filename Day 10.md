# **Why Use Azure CLI?**  

## **1️⃣ Benefits of Azure CLI over UI**  
- **Efficiency:** Creating one VM via the Azure UI is manageable, but for large-scale deployments, CLI is much faster.  
- **Automation:** Azure CLI allows scripting, enabling engineers to store reusable commands in **GitHub** to reduce deployment time.  
- **Scalability:** If a DevOps engineer needs to create multiple **VMs, Kubernetes clusters (AKS), Virtual Networks (VNet), and File Storage**, doing it via UI could take **30+ minutes** per deployment. CLI significantly cuts down this time.  

---

## **2️⃣ Installing Azure CLI**  

### **Steps to Install:**  
1️⃣ **Download & Install** Azure CLI:  
   - Choose **MS Installer** or **MS Installer with PowerShell** (for Windows)  
   - **Download the 64-bit version**  
2️⃣ **Grant necessary permissions** for installation  
3️⃣ **Verify Installation:** Run:  
   ```sh
   az --version
   ```  
4️⃣ **Learn More:** Type **"Learn Azure CLI"** in Azure Docs → Click on **Article List A-Z**  

---

## **3️⃣ Logging into Azure CLI**  
Before creating any resources, you must **log in** to Azure CLI:  
```sh
az login
```  
- This command opens a browser window to authenticate your Azure account.  
- Once authenticated, Azure CLI picks up your **default subscription**.  

---

## **4️⃣ Creating Resources Using Azure CLI**  

### **📌 Creating a Resource Group**  
A **Resource Group** is required as a dependency before creating any resources:  
```sh
az group create --name "MyResourceGroup" --location eastus
```  
- **MyResourceGroup** → Name of the resource group  
- **eastus** → Region where resources will be created  
- ✅ Check the Azure UI to verify that the **Resource Group** is successfully created.  

---

### **📌 Creating a Virtual Machine via CLI**  

Before running the command, define a **PowerShell variable** for the VM name:  
```powershell
$vmName = "TutorialVM1"
```  

Now, create a VM with **Ubuntu 22.04**, inside the specified **VNet and Subnet**:  
```sh
az vm create \
  --resource-group MyResourceGroup \
  --name $vmName \
  --image Ubuntu2204 \
  --vnet-name MyVNet \
  --subnet MySubnet \
  --generate-ssh-keys \
  --output json \
  --verbose
```  
- **--generate-ssh-keys** → If SSH keys don’t exist, they will be created automatically.  
- ✅ Check Azure UI under **Virtual Machines** to see the newly created VM.  

---

### **📌 Creating a Storage Account via Azure CLI**  

Azure Storage Accounts are used to store **blobs (unstructured data), files, tables, and queues**. Let's create one using Azure CLI.  

#### **Step 1: Define Variables**  
Before creating a storage account, we need a **resource group** (which we already created). Define a variable for the storage account name:  
```powershell
$storageAccountName = "mystorageaccount123"  # Must be globally unique
```

#### **Step 2: Create a Storage Account**  
Run the following command:  
```sh
az storage account create \
  --name $storageAccountName \
  --resource-group MyResourceGroup \
  --location eastus \
  --sku Standard_LRS \
  --kind StorageV2 \
  --access-tier Hot
```
🔹 **Breakdown of parameters:**  
- `--name $storageAccountName` → Unique storage account name  
- `--sku Standard_LRS` → Locally Redundant Storage (LRS) for cost-effective redundancy  
- `--kind StorageV2` → Supports **blobs, files, tables, and queues**  
- `--access-tier Hot` → Optimized for frequent access  

✅ **Check in the Azure UI:** Navigate to **Storage Accounts** and verify that the account is created.  

---

## **6️⃣ Working with Different Azure Storage Types**  

### **📌 Creating a Blob Storage Container**  
Blobs are used to store **large unstructured data** like images, videos, and backups.  

```sh
az storage container create \
  --name mycontainer \
  --account-name $storageAccountName \
  --public-access container
```
- **--public-access container** → Allows public access to blobs within the container.  

To upload a file:  
```sh
az storage blob upload \
  --account-name $storageAccountName \
  --container-name mycontainer \
  --name myfile.txt \
  --file /path/to/local/file.txt
```
✅ Verify in **Azure UI → Storage Account → Containers**  

---

### **📌 Creating a File Share**  
File shares allow multiple VMs to **access shared files** in Azure.  

```sh
az storage share create \
  --name myfileshare \
  --account-name $storageAccountName
```
✅ Verify in **Azure UI → Storage Account → File Shares**  

To upload a file:  
```sh
az storage file upload \
  --account-name $storageAccountName \
  --share-name myfileshare \
  --source /path/to/local/file.txt
```

---

### **📌 Creating a Table Storage**  
Azure **Table Storage** is a NoSQL key-value store.  

```sh
az storage table create \
  --name mytable \
  --account-name $storageAccountName
```

---

### **📌 Creating a Queue Storage**  
Queue storage helps in handling **high loads** by queuing requests for processing.  

```sh
az storage queue create \
  --name myqueue \
  --account-name $storageAccountName
```

---

## **7️⃣ Enabling Static Website Hosting in Azure Storage**  
Azure Storage can host **static websites** (HTML, CSS, JavaScript).  

```sh
az storage blob service-properties update \
  --account-name $storageAccountName \
  --static-website \
  --index-document index.html
```
Now upload your **index.html** file:  
```sh
az storage blob upload \
  --account-name $storageAccountName \
  --container-name $web \
  --file /path/to/index.html \
  --name index.html
```
✅ You will see a **primary endpoint URL** in Azure UI. Open this in a browser to see your hosted website!  

---

### **Final Thoughts 💡**
- **Azure CLI** is a powerful tool for automation, scripting, and bulk deployments.  
- **Storage Accounts** allow you to store different types of data efficiently.  
- **Static websites** can be hosted directly from Azure Blob Storage.  

