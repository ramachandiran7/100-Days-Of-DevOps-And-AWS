# Day 96: EC2 Instance with an RSA Key Pair

| | |
|---|---|
| **Day** | 96 of 100 |
| **Phase** | 7 · Terraform |

## 📌 Task

Instance `devops-ec2`, AMI `<AMI_ID>`, `t2.micro`, RSA key pair `devops-kp` (private key saved locally), default security group, all in one `main.tf`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<AMI_ID>`

## ✅ Solution (copy and paste)

```hcl
provider "aws" {
  region = "us-east-1"
}

# RSA key pair
resource "tls_private_key" "devops_key" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

resource "aws_key_pair" "devops_kp" {
  key_name   = "devops-kp"
  public_key = tls_private_key.devops_key.public_key_openssh
}

# Save the private key on disk
resource "local_file" "private_key" {
  content         = tls_private_key.devops_key.private_key_pem
  filename        = "/home/bob/terraform/devops-kp.pem"
  file_permission = "0400"
}

# Default VPC and its default security group
data "aws_vpc" "default" {
  default = true
}

data "aws_security_group" "default" {
  name   = "default"
  vpc_id = data.aws_vpc.default.id
}

resource "aws_instance" "devops_ec2" {
  ami                    = "<AMI_ID>"            # e.g. ami-0c101f26f147fa7fd
  instance_type          = "t2.micro"
  key_name               = aws_key_pair.devops_kp.key_name
  vpc_security_group_ids = [data.aws_security_group.default.id]

  tags = {
    Name = "devops-ec2"
  }
}
```
Run the 5 commands (`init` downloads the `tls` and `local` providers too).

## 🧪 Verification

`ls -l /home/bob/terraform/devops-kp.pem` and `terraform show | grep -A10 devops_ec2`.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `provider tls not found` | Run `terraform init` again. |
| The `.pem` file has wrong permissions | Set `file_permission = "0400"`. |
| `InvalidKeyPair.Duplicate` | The key name exists. Run `terraform destroy` or change the name. |

## 📸 Screenshot

![Day 96 verification](./screenshots/day96.png)

---
[⬅️ Day 95](../DAY95/task-95-create-a-security-group-in-the-default-vpc.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 97 ➡️](../DAY97/task-97-iam-read-only-policy-for-ec2.md)
