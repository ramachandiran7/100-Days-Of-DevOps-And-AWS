# Day 95: Create a Security Group in the Default VPC

| | |
|---|---|
| **Day** | 95 of 100 |
| **Phase** | 7 · Terraform |

## 📌 Task

`xfusion-sg`, description `Security group for Nautilus App Servers`, inbound HTTP 80 and SSH 22 from `0.0.0.0/0`.

## ✅ Solution (copy and paste)

```hcl
provider "aws" {
  region = "us-east-1"
}

data "aws_vpc" "default" {
  default = true
}

resource "aws_security_group" "xfusion_sg" {
  name        = "xfusion-sg"
  description = "Security group for Nautilus App Servers"
  vpc_id      = data.aws_vpc.default.id

  ingress {
    description = "HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    description = "SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "xfusion-sg"
  }
}
```
Run the 5 commands. **Verify:** `terraform show | grep -A12 xfusion_sg`.

## 🧪 Verification

```bash
terraform show
```
The security group `xfusion-sg` is listed with ports 80 and 22.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `DuplicateGroup` | A group with that name exists. Use the task's exact name or run `terraform destroy`. |
| `vpc_id` required | Add the default VPC data source. |
| Rules are wrong | Ports 80 and 22, protocol `tcp`. |

## 📸 Screenshot

![Day 95 verification](./screenshots/day95.png)

---
[⬅️ Day 94](../DAY94/task-94-create-a-vpc.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 96 ➡️](../DAY96/task-96-ec2-instance-with-an-rsa-key-pair.md)
