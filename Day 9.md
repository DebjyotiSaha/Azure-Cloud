
## **Azure Storage Services**  

### **Advantages of Using Microsoft Azure Storage**  
1. **High Durability** → **99.999999999% (11 nines) durability**, ensuring minimal data loss risk.  
2. **High Performance** → Optimized for **fast data access and retrieval**.  
3. **Security** → **Integrated with Azure AD** for role-based access control (RBAC).  

---

### **Types of Azure Storage Services**  

| **Service** | **Use Case** | **Key Features** |
|------------|-------------|------------------|
| **Blob Storage** | Store large unstructured data (images, videos, backups, logs, source code) | **Cost-effective**, supports **hot, cool, and archive tiers** |
| **File Storage** | Share files across multiple VMs or applications | Supports **SMB & NFS protocols**, accessible to **multiple pods in Kubernetes** |
| **Table Storage** | NoSQL data storage for structured, non-relational data | **Key-value store**, **scalable** for big data |
| **Queue Storage** | Store and manage **high-volume application requests** | Ensures **asynchronous message processing**, improves scalability |

✅ **All these storage services are managed within an Azure Storage Account.**  

---

## **How to Create an Azure Storage Account**  

1️⃣ **Go to Azure Portal** → Search **Storage Accounts**  
2️⃣ **Click "Create Storage Account"**  
3️⃣ Provide:  
   - **Subscription & Resource Group**  
   - **Storage Account Name** *(must be unique)*  
   - **Region** *(select nearest for better performance)*  
4️⃣ Click **Create**  

After deployment, click **"Go to Resource"** → This is the **centralized storage location** for managing all storage services.  

---

## **Working with Blob Storage (Container-based Storage)**  

1️⃣ **Go to Storage Account** → Select **Containers**  
2️⃣ Click **"Create Container"** → This represents **Blob Storage**  
3️⃣ Upload files such as **images, videos, or backups**  

---

## **Azure Static Website Hosting**  

Azure Storage also supports **static website hosting**:  

1️⃣ **Go to Storage Account** → Click **Static Website**  
2️⃣ **Enable static website hosting** → Name the file (e.g., `index.html`)  
3️⃣ **Upload HTML file**  
4️⃣ **Retrieve the Primary Endpoint** → This is the **URL to access your website**  

✅ **Useful for hosting static web pages without needing a web server!**  

---
