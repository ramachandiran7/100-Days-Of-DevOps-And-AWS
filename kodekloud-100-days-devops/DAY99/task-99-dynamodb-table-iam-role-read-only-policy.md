# Day 99: DynamoDB Table + IAM Role + Read-Only Policy

| | |
|---|---|
| **Day** | 99 of 100 |
| **Phase** | 7 · Terraform |

## 📌 Task

Table `nautilus-table`, role `nautilus-role` (EC2 trust), policy `nautilus-readonly-policy` (GetItem, Scan, Query on that table), attach policy to role. Use variables, outputs, tfvars. `terraform plan` afterwards must show no changes.

## ✅ Solution (copy and paste)

`variables.tf`
```hcl
variable "region"      { default = "us-east-1" }
variable "table_name"  {}
variable "role_name"   {}
variable "policy_name" {}
```
`terraform.tfvars`
```hcl
table_name  = "nautilus-table"
role_name   = "nautilus-role"
policy_name = "nautilus-readonly-policy"
```
`main.tf`
```hcl
provider "aws" {
  region = var.region
}

resource "aws_dynamodb_table" "table" {
  name         = var.table_name
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "id"

  attribute {
    name = "id"
    type = "S"
  }
}

resource "aws_iam_role" "role" {
  name = var.role_name

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Effect    = "Allow"
      Principal = { Service = "ec2.amazonaws.com" }
      Action    = "sts:AssumeRole"
    }]
  })
}

resource "aws_iam_policy" "readonly" {
  name = var.policy_name

  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Effect   = "Allow"
      Action   = ["dynamodb:GetItem", "dynamodb:Scan", "dynamodb:Query"]
      Resource = aws_dynamodb_table.table.arn
    }]
  })
}

resource "aws_iam_role_policy_attachment" "attach" {
  role       = aws_iam_role.role.name
  policy_arn = aws_iam_policy.readonly.arn
}
```
`outputs.tf`
```hcl
output "table_name"  { value = aws_dynamodb_table.table.name }
output "role_name"   { value = aws_iam_role.role.name }
output "policy_arn"  { value = aws_iam_policy.readonly.arn }
```
```bash
terraform init && terraform validate && terraform apply -auto-approve
terraform plan                           # "No changes."
```

## 🧪 Verification

```bash
terraform plan
```
The plan says `No changes. Your infrastructure matches the configuration.`

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `plan` shows changes after apply | A value differs. Compare the plan output and fix the resource. |
| The role cannot be assumed | The principal service must be `ec2.amazonaws.com`. |
| `ValidationException` on the key | Set the hash key attribute type to `S`. |

## 📸 Screenshot

![Day 99 verification](./screenshots/day99.png)

---
[⬅️ Day 98](../DAY98/task-98-ec2-in-a-private-vpc-subnet-variables-tfvars-outputs.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 100 ➡️](../DAY100/task-100-ec2-cloudwatch-cpu-alarm-to-an-existing-sns-topic.md)
