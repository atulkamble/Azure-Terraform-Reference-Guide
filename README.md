Excellent 👏 You’re asking for a **complete Azure + Terraform Master Reference**, covering everything from **commands and services to interview and practical content**, plus smart **CLI discovery techniques** (so you don’t have to memorize syntax).

Here’s the full structured reference:

---

# 🌩️ **Terraform + Azure — Ultimate Reference Guide (2025 Edition)**

**Author:** Atul Kamble | Cloud Solutions Architect
**Tools:** Terraform | Azure CLI | AzureRM Provider

---

## ⚙️ **1. Terraform Command Reference (All Commands)**

| Category                  | Command                              | Purpose                                |
| ------------------------- | ------------------------------------ | -------------------------------------- |
| **Init & Setup**          | `terraform init`                     | Initialize Terraform working directory |
|                           | `terraform init -upgrade`            | Upgrade provider plugins               |
| **Planning & Validation** | `terraform validate`                 | Validate syntax & configuration        |
|                           | `terraform plan`                     | Show execution plan                    |
|                           | `terraform plan -out=tfplan`         | Save plan to a file                    |
| **Apply & Destroy**       | `terraform apply`                    | Apply configuration                    |
|                           | `terraform apply tfplan`             | Apply from saved plan                  |
|                           | `terraform destroy`                  | Destroy all infrastructure             |
| **Formatting & Docs**     | `terraform fmt`                      | Format code                            |
|                           | `terraform fmt -recursive`           | Format all modules                     |
|                           | `terraform show`                     | Display state or plan                  |
|                           | `terraform graph`                    | Visualize dependencies                 |
| **State Management**      | `terraform state list`               | List all tracked resources             |
|                           | `terraform state show <resource>`    | Show specific resource                 |
|                           | `terraform state rm <resource>`      | Remove from state                      |
|                           | `terraform refresh`                  | Sync state with actual infra           |
| **Workspace Mgmt**        | `terraform workspace list`           | Show all workspaces                    |
|                           | `terraform workspace new dev`        | Create new workspace                   |
| **Providers & Modules**   | `terraform providers`                | List providers used                    |
|                           | `terraform providers mirror ./cache` | Cache providers locally                |
|                           | `terraform get`                      | Download modules                       |
| **Other**                 | `terraform output`                   | Show output values                     |
|                           | `terraform console`                  | Interactive expression shell           |

---

## ☁️ **2. Azure Commands Related to Terraform**

| Purpose                                   | Azure CLI Command                                                                |
| ----------------------------------------- | -------------------------------------------------------------------------------- |
| Login to Azure                            | `az login`                                                                       |
| List subscriptions                        | `az account list -o table`                                                       |
| Set active subscription                   | `az account set --subscription "<ID or Name>"`                                   |
| Create resource group                     | `az group create -n rg-demo -l eastus`                                           |
| Show resource groups                      | `az group list -o table`                                                         |
| Create storage account for remote backend | `az storage account create -n atulstore -g rg-demo -l eastus --sku Standard_LRS` |
| Create container for state file           | `az storage container create -n tfstate --account-name atulstore`                |
| Get storage key                           | `az storage account keys list -g rg-demo -n atulstore -o table`                  |

> 💡 Use these commands to set up Terraform **AzureRM backend**:
>
> ```hcl
> backend "azurerm" {
>   resource_group_name  = "rg-demo"
>   storage_account_name = "atulstore"
>   container_name       = "tfstate"
>   key                  = "terraform.tfstate"
> }
> ```

---

## 🧱 **3. Azure Services & Terraform Code Snippets**

| Service                 | Terraform Resource                                                  | Example                            |
| ----------------------- | ------------------------------------------------------------------- | ---------------------------------- |
| **Resource Group**      | `azurerm_resource_group`                                            | `name="rg-demo"`                   |
| **Virtual Network**     | `azurerm_virtual_network`                                           | `address_space=["10.0.0.0/16"]`    |
| **Subnet**              | `azurerm_subnet`                                                    | `address_prefixes=["10.0.1.0/24"]` |
| **Network Interface**   | `azurerm_network_interface`                                         | Attach to subnet                   |
| **Public IP**           | `azurerm_public_ip`                                                 | `allocation_method="Dynamic"`      |
| **NSG**                 | `azurerm_network_security_group`                                    | Rules for 22, 80, 443              |
| **VM (Linux/Windows)**  | `azurerm_linux_virtual_machine` / `azurerm_windows_virtual_machine` | Define size, admin user            |
| **Storage Account**     | `azurerm_storage_account`                                           | For blobs, queues, tables          |
| **Blob Container**      | `azurerm_storage_container`                                         | `container_access_type="private"`  |
| **App Service**         | `azurerm_app_service`                                               | For web app hosting                |
| **SQL Database**        | `azurerm_mssql_server`, `azurerm_mssql_database`                    | PaaS DB                            |
| **Key Vault**           | `azurerm_key_vault`                                                 | Store secrets & certs              |
| **AKS Cluster**         | `azurerm_kubernetes_cluster`                                        | Azure Kubernetes                   |
| **Load Balancer**       | `azurerm_lb`                                                        | For multi-VM balancing             |
| **Application Gateway** | `azurerm_application_gateway`                                       | Layer 7 load balancer              |
| **DNS Zone**            | `azurerm_dns_zone`, `azurerm_dns_a_record`                          | Manage domains                     |
| **Function App**        | `azurerm_function_app`                                              | Serverless compute                 |
| **Container Registry**  | `azurerm_container_registry`                                        | ACR for Docker images              |

---

## 🧪 **4. Azure Terraform Basic Practicals**

| Practical                  | Description                          |
| -------------------------- | ------------------------------------ |
| 1️⃣ Create Resource Group  | Terraform + `azurerm_resource_group` |
| 2️⃣ Deploy VNet + Subnet   | Network creation & outputs           |
| 3️⃣ Create Linux VM        | SSH access via key pair              |
| 4️⃣ Add NSG Rules          | Allow HTTP/SSH                       |
| 5️⃣ Create Storage Account | Private blob                         |
| 6️⃣ Deploy App Service     | Web App on Linux Plan                |
| 7️⃣ Create SQL Server + DB | Secure with firewall rules           |
| 8️⃣ Create AKS Cluster     | Deploy Nginx                         |
| 9️⃣ Configure Backend      | Remote backend using Azure Storage   |
| 🔟 Use Variables & Outputs | Reuse configs across modules         |

---

## 🎯 **5. Azure Terraform Interview Questions**

**Basic**

* What is the AzureRM provider in Terraform?
* How do you authenticate Terraform with Azure?
* What is the purpose of `terraform.tfstate`?
* How do you handle secrets in Terraform?

**Intermediate**

* How do you manage state files securely in Azure?
* What is the difference between `count` and `for_each`?
* How do you manage multiple environments in Azure with Terraform?
* Explain dependency handling between resources.

**Advanced**

* How do you use remote backends for collaboration?
* What is the difference between `locals` and `variables`?
* How do you import existing Azure resources into Terraform?
* Explain Terraform workspace and its use in Azure CI/CD pipelines.

---

## 🧩 **6. Azure Terraform Scenario-Based Questions**

| Scenario           | Question                                                      |
| ------------------ | ------------------------------------------------------------- |
| 🔐 Secrets         | How to inject Key Vault secrets into AKS cluster?             |
| 🧮 Scaling         | How to scale App Service automatically using Terraform?       |
| ☁️ Networking      | How to peer two VNets in different regions?                   |
| ⚙️ DR Setup        | How to replicate a storage account across regions?            |
| 📈 CI/CD           | How to integrate Terraform in Azure DevOps pipeline?          |
| 🏗️ Multi-env      | How to manage dev, stage, prod environments using workspaces? |
| 🧰 Troubleshooting | What to do if `terraform apply` fails midway?                 |
| 🧾 Governance      | How to enforce tags and policies in all resources?            |

---

## 🧠 **7. CLI Discovery Techniques (No Memory Needed)**

Instead of memorizing every code, use these smart discovery methods:

| Technique                              | Command                                                                                                                                        | What It Does                                   |        |                    |
| -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- | ------ | ------------------ |
| **Find Azure commands**                | `az find "vm create"`                                                                                                                          | Search examples                                |        |                    |
| **List all Azure resource types**      | `az provider list --query "[].namespace" -o table`                                                                                             | Show all services                              |        |                    |
| **List available Terraform resources** | `terraform providers schema -json                                                                                                              | jq '.provider_schemas.azurerm.resource_schemas | keys'` | List all resources |
| **Auto-complete**                      | `az interactive`                                                                                                                               | Launch interactive CLI                         |        |                    |
| **Help on any command**                | `az <service> -h` or `terraform -help`                                                                                                         | Detailed syntax                                |        |                    |
| **Show all provider docs**             | [https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs) | Official reference                             |        |                    |
| **Find resource by keyword**           | Ctrl+F → search resource in registry site                                                                                                      | Quick access to HCL snippets                   |        |                    |

---

## 🧩 **Pro Tip: Azure DevOps Integration**

```yaml
# azure-pipelines.yml
trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- task: TerraformInstaller@1
- script: terraform init
- script: terraform plan
- script: terraform apply -auto-approve
```

---

Would you like me to create this as a **GitHub-ready Markdown document (README.md)** with folder structure and ready-to-practice Terraform code templates (e.g., rg.tf, vm.tf, storage.tf, aks.tf, sql.tf)?
I can also include **100+ Azure Terraform interview & scenario questions** as a separate `.md` file.
