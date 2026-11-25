# Day 94: Create a VPC

| | |
|---|---|
| **Day** | 94 of 100 |
| **Phase** | 7 · Terraform |

## 📌 Task

VPC `xfusion-vpc` in `us-east-1`, any valid CIDR, file `main.tf`.

## ✅ Solution (copy and paste)

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_vpc" "xfusion_vpc" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "xfusion-vpc"
  }
}
```
```bash
terraform init && terraform validate && terraform plan && terraform apply -auto-approve
```

## 🧪 Verification

`terraform show | grep -A3 xfusion` (or `aws ec2 describe-vpcs` if the CLI is configured).

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `terraform init` fails | Check internet access and the provider block. |
| `InvalidVpc.Range` | Use a valid CIDR such as `10.0.0.0/16`. |
| The Name tag is missing | Add `tags = { Name = "xfusion-vpc" }`. |

## 📸 Screenshot

![Day 94 verification](./screenshots/day94.png)

---
[⬅️ Day 93](../DAY93/task-93-conditionals-when.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 95 ➡️](../DAY95/task-95-create-a-security-group-in-the-default-vpc.md)
