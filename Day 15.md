
## 🌐 **Monitoring Azure-hosted Website (example.com) using Kubernetes (KSS)**

The application `example.com` is hosted on Azure and utilizes Azure Kubernetes Services (KSS) for deployment. The KSS architecture is typically divided into two planes:

- **Control Plane (CP)** – Manages the overall state of the cluster.
- **Data Plane (DP)** – Runs the actual application workloads (pods, containers).

To ensure complete observability and monitoring, the Azure architecture is divided into **6 monitoring levels**, each targeting a different aspect of the infrastructure and services.

---

### 🔍 **Monitoring Levels and Tools**

| **Level** | **Description**                          | **Recommended Tool**               |
|-----------|------------------------------------------|------------------------------------|
| **L1**    | Network components (VNet, NSG, Routes)    | ✅ **Azure Network Watcher**        |
| **L2**    | Node pools (VM Scale Sets behind KSS)     | ✅ **Prometheus**                   |
| **L3**    | Control Plane components (API server, etc)| ✅ **Azure Monitor**                |
| **L4**    | Data Plane (Pods, Deployments, Services)  | ✅ **Prometheus + Grafana**         |
| **L5**    | Application Performance Monitoring (APM)  | ✅ **Azure Application Insights**   |
| **L6**    | Other Azure services (e.g., DB, Storage)  | ✅ **Azure Monitor**                |

---

### 📌 **Best Practice**
While Azure provides **a single pane of glass** with unified monitoring tools, it is **not recommended** to rely solely on one tool for all levels. Instead, using **the most effective and specialized tool for each layer** ensures better observability, faster issue resolution, and optimized performance.

---

### 🧠 **Key Takeaways**
- **Prometheus** excels at metrics collection from K8s nodes and workloads.
- **Azure Monitor** integrates well for general metrics, logs, and alerting across Azure resources.
- **Application Insights** is best suited for APM—tracking dependencies, performance bottlenecks, and distributed tracing.
- **Azure Network Watcher** gives visibility into network topology, latency, and flow logs.

---
