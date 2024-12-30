
### **Azure Day 2: Getting Started with Azure**

#### **Azure Account Creation**
- Setting up an Azure account is straightforward.  
- **Benefits for New Users:**
  - First 12 months include free access to select services.
  - $200 credit provided to explore paid services, allowing experimentation with cost-incurring Azure resources.
- **For Students:**  
  Students can register using a valid university ID, enabling access to Azure without requiring credit card information.

---

#### **Regions and Availability Zones**
Azure divides its global infrastructure into **regions** and **availability zones** to ensure low latency and high availability.  

1. **Why Are Data Centers Distributed Globally?**  
   - **Latency** refers to the delay in data transfer between a user and a server.  
   - Example:  
     A startup with clients in France, Germany, and Italy may experience delays if its application is hosted in an Indian data center. This delay occurs because data packets need to travel a great distance, increasing response times.  
   - **Solution:** Azure hosts data centers globally, enabling businesses to deploy applications closer to their users, reducing latency and ensuring seamless experiences.

2. **How Does Azure Address Latency and Downtime?**  
   - Azure strategically divides regions like **US East** and **US West** and sets up multiple data centers in each.  
   - If one region (e.g., US West) faces downtime, the other (e.g., US East) ensures continuity, minimizing disruptions.

---

#### **Service Models in Azure**
Azure offers three primary service models, catering to different business needs:  

1. **IaaS (Infrastructure as a Service):**  
   - Provides virtualized resources such as **VMs**, **storage**, and **networking tools**.  
   - Ideal for businesses that want maximum control over their infrastructure.  

2. **PaaS (Platform as a Service):**  
   - Offers a managed environment for developing and deploying applications, including services like **databases**, **runtime environments**, and **middleware**.  
   - Useful for developers who want to focus on building apps without worrying about managing infrastructure.  

3. **SaaS (Software as a Service):**  
   - Fully managed software solutions provided to end-users.  
   - Examples include email services, CRM tools, or collaboration platforms.  
   - Pricing is typically subscription-based, with Azure charging based on usage or tiers (e.g., $100 for certain services).  

---
