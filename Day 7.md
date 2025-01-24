### **Setting up a VNET, Firewall, Subnet, and Hosting an HTML Page with Nginx on Azure**

Here's a structured walkthrough of the process:

---

#### **1. Create a Resource Group**
- **Why?** A resource group is mandatory for organizing and managing Azure resources.
- Steps:
  1. Go to Azure Portal.
  2. Search for **Resource Groups** and click **Create**.
  3. Provide a **Name** and **Region**.
  4. Click **Review + Create**, then **Create**.

---

#### **2. Create a Virtual Network (VNET)**
- **Why?** VNET ensures logical isolation for resources in Azure.
- Steps:
  1. Search for **Virtual Network** and click **Create**.
  2. Fill in:
     - **Resource Group**: Select the one you just created.
     - **Name**: E.g., `MyVNet`.
     - **Enable Bastion Host**: Check this option.
     - **Create a New Public IP Address** for Bastion. Select **Standard Tier**.
     - **Enable Azure Firewall**: Choose **Basic Tier**.
     - **Firewall Policy**: Create a new one or use the default policy.
  3. In the **IP Addresses** section:
     - 3 subnets will be automatically created: Bastion, Firewall, and Firewall Management.
     - The default **subnet** will be available for deploying applications.
  4. Click **Review + Create**, then **Create**.

---

#### **3. Create a Virtual Machine (VM)**
- **Why?** The VM will host the Nginx server and your static HTML page.
- Steps:
  1. Search for **Virtual Machines** and click **Create**.
  2. Fill in the details:
     - **Resource Group**: Select the same as above.
     - **VM Name**: E.g., `MyVM`.
     - **Region**: Match the VNET region.
     - **Availability Zone**: Choose any.
     - **Image**: Free tier Ubuntu.
     - **Size**: Select a standard free-tier size.
     - **Authentication**: Use **SSH Public Key** and generate a new key pair.
     - **Inbound Port Rules**: Add **SSH (22)**.
  3. Leave **Storage** and **Disks** settings as default.
  4. In **Networking**:
     - Select the **VNET** created earlier.
     - **Subnet**: Choose the default subnet.
     - Disable **Public IP**.
     - Check **Delete NIC when VM is deleted**.
  5. Click **Review + Create**, then **Create**.
  6. Download the `.pem` file (private key).

---

#### **4. Connect to the VM Using Bastion**
- **Why?** Bastion acts as a secure proxy for accessing VMs without public IPs.
- Steps:
  1. Go to the VM in the Azure Portal.
  2. Under the **Connect** tab, choose **Bastion**.
  3. Provide:
     - **Username**: Use the VM's username.
     - **Authentication Type**: Select **SSH Private Key from Local**.
     - Browse and upload the `.pem` file downloaded earlier.
  4. Click **Connect** to access the VM.

---

#### **5. Set Up Nginx and Host the HTML Page**
- **Why?** Nginx is a lightweight web server to host static HTML pages.
- Commands to execute on the VM:
  ```bash
  sudo su -
  apt-get update
  apt-get install nginx -y
  clear
  cd /var/www/html
  vim index.html
  ```
  - Inside the `index.html` file, add the following content:
    ```html
    <h1> I learnt Azure Networking </h1>
    ```
  ```bash
  systemctl restart nginx
  ```

---

#### **6. Configure Firewall DNAT Rules**
- **Why?** DNAT (Destination NAT) rules forward traffic from the firewall to the VM.
- Steps:
  1. Search for **Firewall** in the Azure Portal and select the one created earlier.
  2. Navigate to **Firewall Policy** → **DNAT Rules**.
  3. Click **Add Rule Collection**:
     - **Name**: E.g., `MyDNATRules`.
     - **Type**: DNAT.
     - **Priority**: 100.
  4. Click **Add Rule**:
     - **Name**: E.g., `MyRule`.
     - **Source Type**: IP Address.
     - **Source IP Address**: Enter your IP address (find using `whatismyip.com`).
     - **Destination IP Address**: Public IP of the **Azure Firewall** (can be found in the firewall overview).
     - **Protocol**: TCP.
     - **Port**: 4000.
     - **Translated Type**: IP Address.
     - **Translated Address**: Private IP of the VM.
     - **Translated Port**: 80.
  5. Save the rule.

---

#### **7. Access the HTML Page**
- **How?** 
  - Open a browser.
  - Enter:  
    ```text
    <Azure Firewall Public IP>:4000
    ```
  - You should see your static HTML page displaying:  
    **"I learnt Azure Networking."**

---
