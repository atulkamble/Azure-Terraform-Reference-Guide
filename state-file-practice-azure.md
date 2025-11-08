Perfect — here’s your **Azure-specific version** of the same Terraform State Management hands-on guide 👇

---

# ⚙️ **5. Practice / Hands-On Tasks — Terraform State Management (Azure Edition)**

---

## 🧩 **Task 1: Initialize Terraform and Observe State File Structure**

### Steps

```bash
mkdir terraform-state-lab-azure && cd terraform-state-lab-azure
vim main.tf
```

### Example `main.tf`

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "demo" {
  name     = "rg-tfstate-demo"
  location = "East US"
}
```

### Commands

```bash
terraform init
terraform plan
terraform apply -auto-approve
```

### Observe

* File **`terraform.tfstate`** is created locally.
* View content:

  ```bash
  cat terraform.tfstate | jq .
  # or
  terraform show
  ```

✅  It records the mapping between **Azure resources ⇄ Terraform configuration**.

---

## 🧰 **Task 2: Modify Resource Manually and Run `terraform plan`**

### Example

Go to **Azure Portal → Resource groups → rg-tfstate-demo → change Tags** manually.

Then run:

```bash
terraform plan
```

### Observe

Terraform reports drift:

```
~ resource "azurerm_resource_group" "demo" {
      tags.Name: "OldTag" => "NewTag"
}
```

✅  Terraform compares **state vs actual Azure infrastructure** and flags changes.

---

## ☁️ **Task 3: Configure Remote Backend (Azure Blob Storage)**

### Prerequisite — Create Storage for State

```bash
az group create -n tfstate-rg -l eastus
az storage account create -n atultfstate -g tfstate-rg -l eastus --sku Standard_LRS
az storage container create -n tfstate --account-name atultfstate
```

### Backend Configuration in `main.tf`

```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "tfstate-rg"
    storage_account_name = "atultfstate"
    container_name       = "tfstate"
    key                  = "dev.terraform.tfstate"
  }
}
```

### Commands

```bash
terraform init -migrate-state
```

✅  Local state → Remote Azure Blob.
Verify in **Storage Account > Containers > tfstate**.

---

## 🧱 **Task 4: Move Resource Between Modules using `terraform state mv`**

### Example

You originally had:

```hcl
resource "azurerm_resource_group" "demo" { ... }
```

Now you modularize:

```bash
mkdir -p modules/resourcegroup
mv main.tf modules/resourcegroup/main.tf
```

Then update state:

```bash
terraform state mv azurerm_resource_group.demo module.resourcegroup.azurerm_resource_group.demo
```

✅  Only the **state mapping** changes—no resource recreation.

---

## ♻️ **Task 5: Recover Deleted State Using `.backup` File**

If `terraform.tfstate` is deleted or corrupted:

```bash
ls -la terraform.tfstate*
cp terraform.tfstate.backup terraform.tfstate
terraform plan
```

✅  Terraform re-aligns resources from the backup file.

---

## 🔍 **Summary Table**

| Task | Command / Action                     | Key Learning                          |
| ---- | ------------------------------------ | ------------------------------------- |
| 1    | `terraform init`                     | Creates `.terraform` dir + state file |
| 2    | `terraform plan` after manual change | Detects drift in Azure resources      |
| 3    | Configure Azure Blob backend         | Remote state management               |
| 4    | `terraform state mv`                 | Move resources between modules        |
| 5    | Use `.backup` file                   | Recover state safely                  |

---
