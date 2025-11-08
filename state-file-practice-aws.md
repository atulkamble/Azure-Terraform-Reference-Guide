Excellent practical set ✅ — here’s a **complete guide for your Terraform Hands-On Section (State Management)** — step-by-step with commands, expected behavior, and explanation 👇

---

# ⚙️ **5. Practice / Hands-On Tasks — Terraform State Management**

---

## 🧩 **Task 1: Initialize Terraform and Observe State File Structure**

### Steps

```bash
mkdir terraform-state-lab && cd terraform-state-lab
vim main.tf
```

### Example `main.tf`

```hcl
provider "aws" {
  region = "ap-south-1"
}

resource "aws_s3_bucket" "demo" {
  bucket = "atul-tfstate-demo-bucket"
}
```

### Commands

```bash
terraform init
terraform plan
terraform apply -auto-approve
```

### Observe

* A file named **`terraform.tfstate`** will be created.
* Use:

  ```bash
  cat terraform.tfstate | jq .
  ```

  or

  ```bash
  terraform show
  ```

  ✅ It contains JSON mapping of **real-world resource → Terraform configuration**.

---

## 🧰 **Task 2: Modify Resource Manually and Run `terraform plan`**

### Example

Go to AWS Console → S3 → change the bucket name tag manually.

Then run:

```bash
terraform plan
```

### Observe

Terraform detects **drift**:

```
~ resource "aws_s3_bucket" "demo" {
      tags.Name: "OldName" => "NewName"
}
```

✅ Terraform compares **state file vs actual infrastructure**.

---

## ☁️ **Task 3: Configure Remote Backend (S3 / Azure Blob)**

### Example: **AWS S3 Backend**

```hcl
terraform {
  backend "s3" {
    bucket         = "atul-tf-remote-state"
    key            = "dev/terraform.tfstate"
    region         = "ap-south-1"
    encrypt        = true
  }
}
```

### Example: **Azure Blob Backend**

```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "tfstate-rg"
    storage_account_name = "atultfstate"
    container_name       = "tfstate"
    key                  = "prod.terraform.tfstate"
  }
}
```

### Commands

```bash
terraform init -migrate-state
```

✅ Moves local state → remote storage.
Check your cloud console for the blob or S3 object.

---

## 🧱 **Task 4: Move Resource Between Modules using `terraform state mv`**

### Example

You initially had:

```hcl
resource "aws_s3_bucket" "demo" { ... }
```

Now you create a new folder `modules/s3/main.tf` and move that code there.

Then move state:

```bash
terraform state mv aws_s3_bucket.demo module.s3.aws_s3_bucket.demo
```

✅ This updates only the state file mapping, **without destroying or recreating** resources.

---

## ♻️ **Task 5: Recover Deleted State using `.backup` File**

If `terraform.tfstate` is corrupted or accidentally deleted:

* Check for `.backup`:

  ```bash
  ls -la terraform.tfstate*
  ```
* Restore:

  ```bash
  cp terraform.tfstate.backup terraform.tfstate
  ```
* Validate:

  ```bash
  terraform plan
  ```

✅ Terraform re-aligns your resources using the restored backup.

---

## 🔍 **Summary Table**

| Task | Command / Action                     | Key Learning                            |
| ---- | ------------------------------------ | --------------------------------------- |
| 1    | `terraform init`                     | Creates `.terraform` dir and state file |
| 2    | `terraform plan` after manual change | Detects drift                           |
| 3    | Configure backend                    | Remote state management                 |
| 4    | `terraform state mv`                 | Move resources safely                   |
| 5    | Use `.backup` file                   | State recovery                          |

---
