# Day 100: EC2 + CloudWatch CPU Alarm to an Existing SNS Topic

| | |
|---|---|
| **Day** | 100 of 100 |
| **Phase** | 7 · Terraform |

## 📌 Task

EC2 `nautilus-ec2` (Ubuntu, `t2.micro`, AMI `<AMI_ID>`), alarm `nautilus-alarm`: CPUUtilization, Average, `>= 90` for 1 period of 5 minutes, notify the **existing** SNS topic `nautilus-sns-topic` (reference it, do not create it). Outputs `KKE_instance_name` and `KKE_alarm_name`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<AMI_ID>`

## ✅ Solution (copy and paste)

`main.tf`
```hcl
provider "aws" {
  region = "us-east-1"
}

# Existing SNS topic: look it up
data "aws_sns_topic" "existing" {
  name = "nautilus-sns-topic"
}

resource "aws_instance" "nautilus_ec2" {
  ami           = "<AMI_ID>"            # e.g. ami-0c02fb55956c7d316
  instance_type = "t2.micro"

  tags = {
    Name = "nautilus-ec2"
  }
}

resource "aws_cloudwatch_metric_alarm" "nautilus_alarm" {
  alarm_name          = "nautilus-alarm"
  alarm_description   = "CPU >= 90% for 5 minutes"
  namespace           = "AWS/EC2"
  metric_name         = "CPUUtilization"
  statistic           = "Average"
  comparison_operator = "GreaterThanOrEqualToThreshold"
  threshold           = 90
  period              = 300
  evaluation_periods  = 1

  dimensions = {
    InstanceId = aws_instance.nautilus_ec2.id
  }

  alarm_actions = [data.aws_sns_topic.existing.arn]
}
```
`outputs.tf`
```hcl
output "KKE_instance_name" {
  value = aws_instance.nautilus_ec2.tags["Name"]
}

output "KKE_alarm_name" {
  value = aws_cloudwatch_metric_alarm.nautilus_alarm.alarm_name
}
```
Run the 5 commands. **Verify:** `terraform output` prints both names.

## 🧪 Verification

```bash
terraform output
```
Both `KKE_instance_name` and `KKE_alarm_name` are printed.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `couldn't find resource` for SNS | The name must match exactly: `nautilus-sns-topic`. |
| The alarm does not fire | Check `period`, `threshold`, `statistic` and `evaluation_periods`. |
| Output name is wrong | Use `KKE_instance_name` and `KKE_alarm_name` exactly. |

## 📸 Screenshot

![Day 100 verification](./screenshots/day100.png)

---
[⬅️ Day 99](../DAY99/task-99-dynamodb-table-iam-role-read-only-policy.md) &nbsp;|&nbsp; [🏠 Home](../README.md)
