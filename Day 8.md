

## **1. Difference Between NSG and ASG**  
Both **NSG (Network Security Group)** and **ASG (Application Security Group)** help secure network traffic in Azure, but they serve different purposes:  

| Feature  | NSG (Network Security Group) | ASG (Application Security Group) |
|----------|------------------------------|----------------------------------|
| **Purpose** | Controls traffic using **IP addresses, ports, and protocols** | Controls traffic using **logical application groups** |
| **Use Case** | Block/allow access **between subnets or specific IPs** | Restrict access **between application services in the same subnet** |
| **Example** | Block access from **Login & Logout pages to DB** | Allow only **Processing Page** to access the DB |

---

## **2. How to Block Access to a VM from a Subnet?**  
By default, Azure allows **all subnets within a VNET** to communicate with each other because of an **inbound rule (Priority 65000)**.  

### **Solution**  
1. **Create a custom NSG rule** with **higher priority (e.g., 1000)**.  
2. **Define the source subnet** that should be blocked.  
3. **Apply this rule to the database subnet**, preventing access from unauthorized subnets.  

✅ This ensures **only specific subnets can communicate with the VM** while blocking others.  

---

## **3. Are Azure NSGs Stateful or Stateless?**  
- **NSGs are stateful**: When an inbound request is allowed, the corresponding outbound response is automatically allowed.  
- Example:  
  - If a user requests access to **Jenkins running on a VM**, the NSG allows **inbound HTTP traffic** on the specified port.  
  - The outbound response is **automatically permitted** without needing an additional rule.  

✅ **Stateful NSGs simplify network security by maintaining session awareness.**  

---

## **4. Difference Between Azure Firewall and NSG**  
| Feature  | **Azure Firewall** | **NSG (Network Security Group)** |
|----------|--------------------|----------------------------------|
| **Scope** | Controls traffic at **VNET level** | Controls traffic at **subnet/VM level** |
| **Filtering** | Deep packet inspection, FQDN filtering, and threat intelligence | Basic filtering using **IP, Port, and Protocol** |
| **Use Case** | Secure traffic between VNETs, hybrid networks, and external connections | Restrict or allow access between **VMs and subnets** |

✅ **NSG protects individual resources, whereas Azure Firewall secures entire networks.**  

---

## **5. Advantages of Azure Resource Groups**  
- **Logical Organization** → Group related resources for better management.  
- **Access Control** → Assign different permissions at the **resource group level**.  
- **Cost Optimization** → Monitor and track resource usage for specific projects.  
- **Simplified Deployment** → Automate infrastructure deployment using **ARM templates**.  

✅ **Resource Groups help in better cost control, security, and resource tracking.**  

---

## **6. Difference Between Azure User Data and Custom Data**  
| Feature  | **User Data** | **Custom Data** |
|----------|-------------|-----------------|
| **Purpose** | Runs startup scripts during **VM provisioning** | Stores configuration data **for applications** |
| **Execution** | **Automatically executed** at first boot | **Not executed**, needs manual retrieval |
| **Example** | Install **Apache** on VM startup | Store a **configuration file** for an application |

✅ **User Data is used for automation, whereas Custom Data is static information stored in a VM.**  

---

## **7. Difference Between Azure App Gateway and Load Balancer**  
| Feature | **App Gateway (Layer 7 - HTTP/HTTPS)** | **Load Balancer (Layer 4 - TCP/UDP)** |
|---------|------------------------------------|----------------------------------|
| **Routing Based On** | URLs, HTTP headers, cookies | IP address and ports |
| **Security Features** | WAF (Web Application Firewall) protection | No security filtering |
| **Use Case** | Web applications, HTTPS-based traffic | Backend applications, databases, fast IP-based routing |

✅ **Use App Gateway for web apps and Load Balancer for backend infrastructure.**  

---

## **8. Traffic Flow in Azure Networking**  
### **Scenario**: A user accesses a web application hosted in an Azure VNET.  

1️⃣ **User enters the website URL** → DNS resolves to the **Azure Firewall Public IP**.  
2️⃣ **Azure Firewall (NAT Rule)** → Routes the request securely.  
3️⃣ **App Gateway (L7 Load Balancer)** → Directs traffic to the appropriate web server.  
4️⃣ **NSG (Network Security Group)** → Ensures only allowed traffic reaches the web app.  
5️⃣ **Bastion (Secure DevOps Access)** → Allows DevOps engineers to manage the VM without exposing SSH/RDP publicly.  

✅ **This setup ensures security at multiple levels: firewall, NSG, and bastion.**  

---

## **9. What is Azure Bastion & Why is it Secure?**  
- **Azure Bastion** provides **secure RDP/SSH access** to VMs **without exposing public IPs**.  
- **Why is it secure?**  
  - Eliminates **direct SSH/RDP access** from the internet.  
  - Uses **Azure Portal for access**, reducing attack surface.  
  - Prevents **brute-force attacks** on VMs.  

✅ **Bastion enhances security by acting as a proxy for remote access to VMs.**  

---

