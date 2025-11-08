👏 a **Complete Azure + Terraform Master Reference**, covering everything from **commands and services to interview and practical content**, plus smart **CLI discovery techniques** (so you don’t have to memorize syntax).

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

clear and practical explanation of **basic Terraform file structures** 🧩 — along with their **significance and best practices** for real-world Azure/AWS/DevOps projects.

---

# 🌍 **Terraform Basic File Structure & Significance**

Terraform organizes infrastructure as code (IaC) in a **modular and declarative** format.
A typical Terraform project contains several core files — each serving a specific purpose.

---

## 📁 **1. Root Project Folder**

Example:

```
terraform-azure-demo/
│
├── main.tf
├── variables.tf
├── outputs.tf
├── provider.tf
├── terraform.tfvars
├── versions.tf
├── backend.tf
└── README.md
```

---

## 📘 **2. File Breakdown**

| File                 | Purpose                                   | Example / Description                                                                                                                     |
| -------------------- | ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **main.tf**          | Core infrastructure definitions           | Contains **resource** blocks — e.g., `azurerm_resource_group`, `aws_instance`, etc.                                                       |
| **provider.tf**      | Defines cloud provider and authentication | Example: `provider "azurerm" { features {} subscription_id = "..." }`                                                                     |
| **variables.tf**     | Declares all input variables              | Keeps configuration **flexible** and **reusable**. Example: `variable "location" { default = "eastus" }`                                  |
| **terraform.tfvars** | Stores variable values                    | Example: `location = "eastus"`; overrides defaults from `variables.tf`                                                                    |
| **outputs.tf**       | Defines output values after deployment    | Example: `output "resource_group_name" { value = azurerm_resource_group.demo.name }`                                                      |
| **versions.tf**      | Specifies Terraform & provider versions   | Example: `terraform { required_version = ">= 1.5.0" required_providers { azurerm = { source = "hashicorp/azurerm", version = ">=3.0" }}}` |
| **backend.tf**       | Configures remote backend (state storage) | Example: store state in **Azure Storage**, **S3**, or **Terraform Cloud**                                                                 |
| **README.md**        | Project documentation                     | Explains setup, commands, and resources created                                                                                           |

---

## 🧱 **3. Optional (Advanced) Structure**

For large-scale or production projects:

```
terraform-project/
│
├── modules/
│   ├── network/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── README.md
│   └── compute/
│       ├── main.tf
│       ├── variables.tf
│       ├── outputs.tf
│       └── README.md
│
├── environments/
│   ├── dev/
│   │   └── terraform.tfvars
│   ├── staging/
│   │   └── terraform.tfvars
│   └── prod/
│       └── terraform.tfvars
│
├── main.tf
├── provider.tf
├── versions.tf
└── backend.tf
```

### 🔹 Significance

* **modules/** → Reusable blueprints for resources (e.g., VMs, VPCs, VNets).
* **environments/** → Separate configs for dev/staging/prod using same module.
* Encourages **scalability, reusability, and CI/CD automation**.

---

## 🪄 **4. Additional Supporting Files**

| File                         | Use Case                                                                  |
| ---------------------------- | ------------------------------------------------------------------------- |
| **.terraform/**              | Auto-created directory containing provider plugins and state lock files   |
| **.terraform.lock.hcl**      | Locks provider versions to ensure consistency across machines             |
| **.gitignore**               | Exclude `.terraform/`, `*.tfstate`, and secret files from version control |
| **terraform.tfstate**        | Stores actual deployed infrastructure state (NEVER edit manually!)        |
| **terraform.tfstate.backup** | Automatic backup of the last known good state                             |

---

## 🧭 **5. Recommended Development Order**

1. `versions.tf` → define Terraform & provider version
2. `provider.tf` → configure cloud provider
3. `variables.tf` → define input parameters
4. `main.tf` → write resources
5. `outputs.tf` → export key values
6. `terraform.tfvars` → add real values
7. `backend.tf` → configure remote state (for teams)
8. Run:

   ```bash
   terraform init
   terraform plan
   terraform apply
   ```

---

## 🚀 **6. Example Mini Project (Azure)**

**main.tf**

```hcl
resource "azurerm_resource_group" "rg" {
  name     = var.rg_name
  location = var.location
}
```

**variables.tf**

```hcl
variable "rg_name" { type = string }
variable "location" { default = "eastus" }
```

**terraform.tfvars**

```hcl
rg_name = "demo-rg"
```

**outputs.tf**

```hcl
output "rg_id" {
  value = azurerm_resource_group.rg.id
}
```

---
In a Terraform project, **hidden files and folders** (those starting with `.`) are created automatically to manage backend state, provider credentials, and module caching. Here’s what they mean 👇

---

## 🧩 **Terraform Hidden Files and Folders**

### 1. `.terraform/` (hidden directory)

This is created when you run `terraform init`.
It stores **plugins, modules, and provider configurations**.

**Contents inside `.terraform/`:**

| Folder                            | Description                                                                                               |
| --------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `.terraform/providers/`           | Provider plugins downloaded from the Terraform Registry (e.g., `registry.terraform.io/hashicorp/azurerm`) |
| `.terraform/modules/`             | Cached Terraform modules used in your project                                                             |
| `.terraform/environment`          | Tracks the selected workspace/environment                                                                 |
| `.terraform.lock.hcl` (see below) | Dependency lock file for provider versions                                                                |

---

### 2. `.terraform.lock.hcl`

This is a **lock file** created by Terraform to ensure **provider version consistency**.

**Purpose:**

* Prevents unexpected version upgrades
* Ensures the same provider versions are used across all environments

**Example snippet:**

```hcl
provider "registry.terraform.io/hashicorp/azurerm" {
  version = "3.105.0"
  hashes = [
    "h1:abc123xyz...",
    "zh:abcd..."
  ]
}
```

---

### 3. `.terraform.tfstate` (and `.backup`)

While not hidden, it’s **critical** for Terraform to track real infrastructure.

| File                       | Purpose                                             |
| -------------------------- | --------------------------------------------------- |
| `terraform.tfstate`        | Stores the current state of your deployed resources |
| `terraform.tfstate.backup` | Automatic backup of the previous state file         |

👉 Best practice:
Never manually edit or commit these files to Git.
Add them to `.gitignore` (see below).

---

### 4. `.gitignore` (manual file)

A hidden file you create to exclude sensitive Terraform files from version control.

**Recommended `.gitignore` for Terraform:**

```
# Local .terraform directories
.terraform/

# State files
*.tfstate
*.tfstate.*

# Crash log
crash.log

# Sensitive variable files
*.tfvars
*.tfvars.json

# Lock file
.terraform.lock.hcl
```

---

### 🧠 Quick Tip — View Hidden Files

**Linux/macOS:**

```bash
ls -a
```

**Windows PowerShell:**

```powershell
Get-ChildItem -Force
```

---
Excellent and practical question ✅ — this is something every Terraform practitioner should master while working with **Azure CLI + Terraform (AzureRM provider)**.

Let’s go step-by-step 👇

---

# 🌩️ **How to Get Azure Parameters & References from CLI While Practicing Terraform**

---

## 🧩 1️⃣ **Understand What “Parameters” Means in Terraform for Azure**

When writing Terraform code for Azure, you often need:

* **Subscription ID**
* **Resource Group name**
* **Location (Region)**
* **VNet / Subnet / NSG / Storage account names**
* **SKU / Tier / Size / ID references**
* **Principal IDs / Object IDs for roles**

👉 All of these can be fetched directly using `az` commands.

---

## 🧰 2️⃣ **General Azure CLI Commands to Get Terraform Inputs**

| Resource Type             | Azure CLI Command                                                               | Terraform Equivalent Variable    |
| ------------------------- | ------------------------------------------------------------------------------- | -------------------------------- |
| Subscription ID           | `az account show --query id -o tsv`                                             | `subscription_id`                |
| Tenant ID                 | `az account show --query tenantId -o tsv`                                       | `tenant_id`                      |
| Resource Group list       | `az group list -o table`                                                        | used in `resource_group_name`    |
| Regions list              | `az account list-locations -o table`                                            | used in `location`               |
| VNet list                 | `az network vnet list -o table`                                                 | `vnet_name`                      |
| Subnet list               | `az network vnet subnet list --vnet-name myvnet --resource-group myrg -o table` | `subnet_id`                      |
| Storage accounts          | `az storage account list -o table`                                              | `storage_account_name`           |
| VM sizes per region       | `az vm list-sizes --location eastus -o table`                                   | used in `vm_size`                |
| Available images          | `az vm image list --publisher Canonical --offer UbuntuServer --all -o table`    | used in `source_image_reference` |
| Service principal details | `az ad sp list --display-name mysp -o table`                                    | for `client_id`, `object_id`     |

---

## ⚙️ 3️⃣ **Example: Use Azure CLI to Populate Terraform Variables**

### Example 1 — Get Subscription and Tenant IDs

```bash
export ARM_SUBSCRIPTION_ID=$(az account show --query id -o tsv)
export ARM_TENANT_ID=$(az account show --query tenantId -o tsv)
```

These environment variables are **automatically picked by Terraform** provider block if not hardcoded.

---

### Example 2 — Get Region and Resource Group Name

```bash
az account list-locations -o table
az group list -o table
```

Then use:

```hcl
location            = "eastus"
resource_group_name = "demo-rg"
```

---

### Example 3 — Get IDs for Existing Resources

You can fetch **resource IDs** directly for use in references:

```bash
az network vnet show -g demo-rg -n demo-vnet --query id -o tsv
az network vnet subnet show -g demo-rg --vnet-name demo-vnet -n default --query id -o tsv
```

Use inside Terraform:

```hcl
subnet_id = "paste-output-id-here"
```

---

## 💡 4️⃣ **Bonus: Get Terraform Reference Codes / Schema**

To find out all possible Terraform attributes for any Azure resource:

### Option 1 — Use Terraform CLI

```bash
terraform providers schema -json | jq '.provider_schemas."registry.terraform.io/hashicorp/azurerm"'
```

### Option 2 — Open Docs Quickly from CLI

```bash
terraform docs show -provider azurerm
```

Or visit:
🔗 [https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)

---

## ⚡ 5️⃣ **Get Azure IDs and References via Data Sources**

If a resource already exists, use Terraform **data blocks** to import its properties dynamically instead of using CLI:

```hcl
data "azurerm_resource_group" "example" {
  name = "demo-rg"
}

data "azurerm_virtual_network" "example" {
  name                = "demo-vnet"
  resource_group_name = data.azurerm_resource_group.example.name
}

output "vnet_id" {
  value = data.azurerm_virtual_network.example.id
}
```

Then run:

```bash
terraform apply
```

✅ Terraform automatically queries Azure API using provider credentials (same as CLI).

---

## 🧠 6️⃣ **Pro Technique — Don’t Memorize Codes**

Use these practical tricks:

* `az <service> -h` → shows all CLI parameters
  Example:

  ```bash
  az network vnet create -h
  ```
* Copy `--name`, `--resource-group`, etc., to create Terraform equivalent fields.
* Use:

  ```bash
  az resource show --ids <resource_id> --query '{name:name, id:id, type:type}'
  ```

  to get all references for Terraform import or existing infra.

---

## 🪄 7️⃣ **Terraform Import + CLI Combination**

When you have an existing Azure resource:

```bash
az resource show -g demo-rg -n demo-vnet --resource-type Microsoft.Network/virtualNetworks
```

Then:

```bash
terraform import azurerm_virtual_network.demo "/subscriptions/xxx/resourceGroups/demo-rg/providers/Microsoft.Network/virtualNetworks/demo-vnet"
```

---

## 🧭 Summary Cheat Sheet

| Type             | Command                                                                 |
| ---------------- | ----------------------------------------------------------------------- |
| All regions      | `az account list-locations -o table`                                    |
| Resource Groups  | `az group list -o table`                                                |
| VMs              | `az vm list -o table`                                                   |
| Images           | `az vm image list --publisher Canonical --offer UbuntuServer -o table`  |
| Sizes            | `az vm list-sizes --location eastus -o table`                           |
| Networks         | `az network vnet list -o table`                                         |
| Subnets          | `az network vnet subnet list -g demo-rg --vnet-name demo-vnet -o table` |
| Disks            | `az disk list -o table`                                                 |
| Storage Accounts | `az storage account list -o table`                                      |

---


