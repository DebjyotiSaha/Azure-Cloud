# **📌 Understanding Azure IAM (Identity and Access Management) & Role-Based Access Control (RBAC)**  

Azure **IAM (Identity and Access Management)** ensures secure access to resources by handling **Authentication** and **Authorization**:  
🔹 **Authentication** → Verifies **who** you are. (Handled using **Azure Entra ID**)  
🔹 **Authorization** → Determines **what** you can do. (Managed using **Roles & Role Assignments**)  

---

## **1️⃣ Key Concepts of Azure IAM**  
### ✅ **Authentication – Managing Users & Groups**  
- Users are **grouped** into **Azure AD Groups** for easier management.  
- Groups are used to **assign permissions collectively** instead of user-by-user access.  

### ✅ **Authorization – Assigning Roles**  
- **Roles** define permissions (e.g., Read-Only, Contributor, Virtual Machine Operator).  
- Azure **RBAC (Role-Based Access Control)** ensures users **only access what they need**.  

---

## **2️⃣ Creating an Identity in Azure Entra ID**  

### **🔹 Step 1: Create an Azure Entra ID User**
1️⃣ **Go to Azure Portal** → Search for **"Entra ID"**  
2️⃣ **Navigate to** *Users* → Click **"New User"**  
3️⃣ Provide:  
   - **User Name**  
   - **Password** (Auto-generated)  
   - **Assign a Group** (Optional but recommended)  
4️⃣ Click **Create**  

### **🔹 Step 2: Assign a Role to the User**
1️⃣ Go to **Entra ID** → *Users*  
2️⃣ Select the **User** → Click on **"Assigned Roles"**  
3️⃣ Click **"Add Role Assignment"**  
4️⃣ Choose a **Built-in Role** (e.g., Virtual Machine Contributor, Storage Account Reader)  
5️⃣ Click **Assign**  

✅ Now, the user has **limited access** based on the assigned role.  

---

## **3️⃣ Creating an Identity from CLI**  

### **🔹 Step 1: Create a Resource Group**
```sh
az group create --name MyResourceGroup --location eastus
```

### **🔹 Step 2: Create a New User in Azure Entra ID**
```sh
az ad user create \
  --display-name "John Doe" \
  --user-principal-name "johndoe@yourdomain.onmicrosoft.com" \
  --password "SecureP@ssw0rd!"
```
🔹 **User principal name (UPN)** must follow `@yourdomain.onmicrosoft.com`.  

### **🔹 Step 3: Assign a Role to the User**
```sh
az role assignment create \
  --assignee johndoe@yourdomain.onmicrosoft.com \
  --role "Reader" \
  --scope /subscriptions/YOUR_SUBSCRIPTION_ID/resourceGroups/MyResourceGroup
```
🔹 This grants the **Reader** role to `johndoe` for the resource group.  

### **🔹 Step 4: List Role Assignments for a User**
```sh
az role assignment list --assignee johndoe@yourdomain.onmicrosoft.com
```
✅ This command shows all the **permissions** assigned to `johndoe`.  

---

## **4️⃣ How IAM Works in Real-World Azure Environments**
**🔹 Scenario:** You want to give your developer **read-only access** to a Virtual Machine.  
- **Step 1:** Create an Entra ID user.  
- **Step 2:** Assign them **"Virtual Machine Reader"** role.  
- **Step 3:** Verify that they can see VM details but **cannot modify them**.  

---

## **5️⃣ Benefits of Azure IAM & RBAC**  
✔ **Least Privilege Access** → Users get **only the permissions** they need.  
✔ **Secure & Centralized Management** → Everything managed via **Azure Entra ID**.  
✔ **Easy Auditing & Compliance** → Track & manage role assignments efficiently.  

