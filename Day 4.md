### **Azure Day 4: Virtual Machines (VMs)**

#### **What is Virtualization?**
- Virtualization is the process of dividing a physical server into multiple virtual servers using hypervisor software.  
- Azure leverages virtualization by installing hypervisors on physical servers in specific zones. These servers are then divided into virtual servers, which are assigned based on user requests.

---

#### **Creating a Virtual Machine (VM) in Azure**

1. **Accessing VM Creation in Azure:**  
   - In the Azure Portal, search for "Virtual Machine" in the search bar.  
   - Click on the "Create" option to start configuring your VM.

2. **Configuration Details:**  
   - **Subscription:** Choose between Free Trial or Paid.  
   - **Resource Group:** Create one from the Resource Group service in Azure by providing a group name.  
   - **VM Name:** Assign a name to the virtual machine.  
   - **Region:** Select a region to host your VM.  
   - **Availability Zone:** Choose one of the three zones.  
   - **Image:** Select an operating system (e.g., Ubuntu). Free options are available.  
   - **Architecture:** Use `x64`.  
   - **Size:** Select a free tier for demo purposes.  
   - **Authentication Type:**  
     - Choose **SSH Key Pair**.  
     - Enter a username, generate a key pair, and provide a name for the key pair.  

3. **Finalize Creation:**  
   - Click on **Review and Create** to validate the settings.  
   - Download the private key file for accessing the VM.

---

#### **Accessing the Virtual Machine**
1. **Retrieve Public IP Address:**  
   - Go to the **Home** section of Azure, locate your VM, and copy its public IP address.

2. **Connect Using SSH (Recommended):**  
   - Install **Git Bash** (Windows users) for SSH access.  
   - Command to connect:  
     ```bash
     ssh -i path_to_private_key/key_name.pem azureuser@public_IP_address
     ```  
   - If you receive a permission error for the `.pem` file, modify the file permissions:  
     ```bash
     chmod 600 path_to_private_key/key_name.pem
     ```

3. **Alternative: Azure Cloud Shell:**  
   - Access via the Azure Portal, though not recommended for regular use.

---

#### **Installing Jenkins on the VM**
1. Use GitHub (e.g., Abhishek Veramalla’s Jenkins page) to get Linux commands for installation.  
2. Verify Jenkins is running using the command:  
   ```bash
   ps -ef | grep Jenkins
   ```  
   - Note the port Jenkins is using.  

3. **Open Ports in Azure:**  
   - Navigate to **Network Security Group** -> **Inbound Port Rules** -> Add a rule to open the necessary port.

---

#### **Virtual Machine Scale Sets (VMSS)**
- **What is VMSS?**  
   VMSS allows for automatic scaling of virtual machines to handle fluctuating traffic loads. It ensures high availability and application reliability by dynamically creating and configuring VMs as needed.

---

#### **Types of Azure Virtual Machines**
Azure offers several types of VMs to address different workloads and performance requirements:  

1. **General-Purpose VMs**  
   - **Example:** `Standard_D2s_v3`  
   - **Description:** Balanced CPU-to-memory ratio.  
   - **Use Case:** Development, testing, and hosting lightweight applications.

2. **Compute-Optimized VMs**  
   - **Example:** `Standard_F2s_v2`  
   - **Description:** High CPU-to-memory ratio for compute-heavy tasks.  
   - **Use Case:** Batch processing, gaming applications.

3. **Memory-Optimized VMs**  
   - **Example:** `Standard_E16s_v3`  
   - **Description:** High memory-to-CPU ratio.  
   - **Use Case:** Large databases, in-memory caching.

4. **Storage-Optimized VMs**  
   - **Example:** `Standard_L8s_v2`  
   - **Description:** Optimized for storage throughput and I/O performance.  
   - **Use Case:** Big data applications.

5. **GPU VMs**  
   - **Example:** `Standard_NC6s_v3`  
   - **Description:** Equipped with GPUs for graphics and machine learning.  
   - **Use Case:** Graphics rendering, simulations.

6. **High-Performance Compute VMs**  
   - **Example:** `Standard_H16r`  
   - **Description:** Built for parallel processing and HPC tasks.  
   - **Use Case:** Simulations, modeling.

7. **Burstable VMs**  
   - **Example:** `B1s`  
   - **Description:** Cost-effective with the ability to handle variable workloads.  
   - **Use Case:** Small websites, development environments.

---
