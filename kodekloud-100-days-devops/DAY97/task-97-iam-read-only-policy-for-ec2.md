# Day 97: IAM Read-Only Policy for EC2

| | |
|---|---|
| **Day** | 97 of 100 |
| **Phase** | 7 · Terraform |

## 📌 Task

Policy `iampolicy_jim`: read-only view of EC2 instances, AMIs and snapshots.

## ✅ Solution (copy and paste)

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_iam_policy" "iampolicy_jim" {
  name        = "iampolicy_jim"
  description = "Read-only access to EC2 instances, AMIs and snapshots"

  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Effect = "Allow"
        Action = [
          "ec2:Describe*",
          "ec2:GetConsole*"
        ]
        Resource = "*"
      }
    ]
  })
}
```
Run the 5 commands. **Verify:** `terraform show | grep -A15 iampolicy_jim`.

## 🧪 Verification

```bash
terraform show
```
The policy `iampolicy_jim` is listed with the EC2 read actions.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `MalformedPolicyDocument` | The JSON structure is wrong. Use `jsonencode` as in the solution. |
| The policy name differs | Use the exact name `iampolicy_jim`. |
| Wrong actions | Use the actions listed in the task. |

## 💡 Notes

`ec2:Describe*` covers `DescribeInstances`, `DescribeImages` and `DescribeSnapshots`. If the task lists exact actions, write those instead.

## 📸 Screenshot

![Day 97 verification](./screenshots/day97.png)

---
[⬅️ Day 96](../DAY96/task-96-ec2-instance-with-an-rsa-key-pair.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 98 ➡️](../DAY98/task-98-ec2-in-a-private-vpc-subnet-variables-tfvars-outputs.md)
