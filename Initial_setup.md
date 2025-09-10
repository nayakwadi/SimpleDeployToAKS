
---

````md
# 🛠️ Local Development Environment Setup for Azure + Kubernetes

This guide outlines the steps to set up a local development environment for working with Azure, Kubernetes (AKS), and Docker.

---

## 📦 Prerequisites Installation

1. **Install Visual Studio 2022 Community Edition**  
   [Download VS 2022](https://apps.microsoft.com/detail/xpdcfjdklzjlp8?launch=true&mode=full&hl=en-us&gl=us&ocid=bingwebsearch)

2. **Install Visual Studio Code (VS Code)**  
   [Download VS Code](https://apps.microsoft.com/detail/xp9khm4bk9fz7q?launch=true&mode=full&hl=en-us&gl=us&ocid=bingwebsearch)

3. **Install Azure CLI**  
   [Azure CLI Installation Guide (Windows)](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest&pivots=msi#microsoft-installer-msi)

4. **Enable Windows Subsystem for Linux (WSL)**  
   - Open **Command Prompt** and run:
     ```sh
     wsl --version
     ```
   - Follow instructions in the prompt to install WSL if not already available.

5. **Install Docker Desktop**  
   - After installation, verify it with:
     ```sh
     docker --version
     ```

6. **Install kubectl (Kubernetes CLI)**  
   [kubectl Installation Guide](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/)

---

## ☁️ Azure Setup

7. **Create Azure Subscription and Resource Group**
   - Use the [Azure Portal](https://portal.azure.com)
   - Create:
     - A subscription (if not already present)
     - A Resource Group (RG)

8. **Register Required Azure Resource Providers**

   - Open **VS Code Terminal** or any terminal with Azure CLI.
   - Run the following commands:

   ```bash
   az login
   az account set --subscription <subscriptionId>

   # Register required resource providers (takes a few minutes)
   az provider register --namespace Microsoft.Insights --wait
   az provider register --namespace Microsoft.OperationalInsights --wait
   az provider register --namespace Microsoft.ContainerService --wait
   az provider register --namespace Microsoft.Network --wait
   az provider register --namespace Microsoft.Compute --wait
   az provider register --namespace Microsoft.OperationsManagement --wait
   az provider register --namespace Microsoft.Authorization --wait
   az provider register --namespace Microsoft.Storage --wait
   az provider register --namespace Microsoft.ContainerRegistry --wait
````

9. **Create an Azure Container Registry (ACR)**

   ```bash
   az acr create --resource-group <RGNAME> --name <ACRNAME> --sku basic
   ```

10. **Create an Azure Kubernetes Service (AKS) Cluster**

```bash
az aks create \
  --resource-group <RGNAME> \
  --name <AKS_CLUSTER_NAME> \
  --node-count 1 \
  --node-vm-size Standard_B2s \
  --enable-addons monitoring \
  --generate-ssh-keys
```

---

## 🔧 Kubernetes Configuration

11. **Get AKS Credentials**

> Navigate to the directory containing the `.kube` folder.

```bash
az aks get-credentials --resource-group <RGNAME> --name <AKS_CLUSTER_NAME>
```

12. **Check Cluster Info**

```bash
kubectl cluster-info
```

13. **Check Current Kubernetes Context**

> The `.kube/config` file stores context information.

```bash
kubectl config current-context
```

14. **Basic Kubernetes CLI Commands**

```bash
kubectl get nodes
kubectl get namespaces
```

> ⚠️ By default, user workloads are deployed in the `default` namespace. You can create custom namespaces if needed.

15. Link the AKS cluster with Container Registry by running below command in VS Code.(This will take 40+ minutes)
``` bash
   az aks update --resource-group <RG_NAME> --name <AKS_CLUSTER_NAME> --attach-acr <ACR_NAME>
```
---

