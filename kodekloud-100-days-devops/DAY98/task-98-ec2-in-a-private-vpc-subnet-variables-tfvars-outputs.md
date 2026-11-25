# Day 98: EC2 in a Private VPC Subnet (variables, tfvars, outputs)

| | |
|---|---|
| **Day** | 98 of 100 |
| **Phase** | 7 · Terraform |

## 📌 Task

VPC `xfusion-priv-vpc` (10.0.0.0/16), subnet `xfusion-priv-subnet` (10.0.1.0/24, no public IP), EC2 `xfusion-priv-ec2` (`t2.micro`), security group allowing only the VPC CIDR. Use `variables.tf`, `terraform.tfvars`, `outputs.tf`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<AMI_ID>`

## ✅ Solution (copy and paste)

`variables.tf`
```hcl
variable "region"        { default = "us-east-1" }
variable "vpc_name"      {}
variable "vpc_cidr"      {}
variable "subnet_name"   {}
variable "subnet_cidr"   {}
variable "instance_name" {}
variable "ami_id"        {}
variable "instance_type" { default = "t2.micro" }
```
`terraform.tfvars`
```hcl
vpc_name      = "xfusion-priv-vpc"
vpc_cidr      = "10.0.0.0/16"
subnet_name   = "xfusion-priv-subnet"
subnet_cidr   = "10.0.1.0/24"
instance_name = "xfusion-priv-ec2"
ami_id        = "<AMI_ID>"
```
`main.tf`
```hcl
provider "aws" {
  region = var.region
}

resource "aws_vpc" "priv_vpc" {
  cidr_block = var.vpc_cidr
  tags       = { Name = var.vpc_name }
}

resource "aws_subnet" "priv_subnet" {
  vpc_id                  = aws_vpc.priv_vpc.id
  cidr_block              = var.subnet_cidr
  map_public_ip_on_launch = false
  tags                    = { Name = var.subnet_name }
}

resource "aws_security_group" "priv_sg" {
  name        = "xfusion-priv-sg"
  description = "Allow traffic only from inside the VPC"
  vpc_id      = aws_vpc.priv_vpc.id

  ingress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = [var.vpc_cidr]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

resource "aws_instance" "priv_ec2" {
  ami                         = var.ami_id
  instance_type               = var.instance_type
  subnet_id                   = aws_subnet.priv_subnet.id
  vpc_security_group_ids      = [aws_security_group.priv_sg.id]
  associate_public_ip_address = false
  tags                        = { Name = var.instance_name }
}
```
`outputs.tf`
```hcl
output "vpc_id"      { value = aws_vpc.priv_vpc.id }
output "subnet_id"   { value = aws_subnet.priv_subnet.id }
output "instance_id" { value = aws_instance.priv_ec2.id }
output "private_ip"  { value = aws_instance.priv_ec2.private_ip }
```
Run the 5 commands. **Verify:** `terraform output` and confirm no public IP.

## 🧪 Verification

```bash
terraform output
terraform show
```
The outputs show the VPC, subnet and instance IDs, and the instance has no public IP.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `No value for required variable` | Add it to `terraform.tfvars`. |
| The instance has a public IP | Set `map_public_ip_on_launch = false` and `associate_public_ip_address = false`. |
| An output is missing | Check the names in `outputs.tf` against the task. |

## 💡 Notes

output names must match what your task asks for, if it names any.

## 📸 Screenshot

![Day 98 verification](./screenshots/day98.png)

---
[⬅️ Day 97](../DAY97/task-97-iam-read-only-policy-for-ec2.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 99 ➡️](../DAY99/task-99-dynamodb-table-iam-role-read-only-policy.md)
