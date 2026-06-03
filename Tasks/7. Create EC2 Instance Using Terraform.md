# Day 07 – Create EC2 Instance Using Terraform

---

## Task Overview

The Nautilus DevOps team is provisioning compute resources on AWS using Terraform. The requirement is to launch an EC2 instance with a specific AMI and instance type.

---

# Objective

| Property      | Value                   |
| ------------- | ----------------------- |
| Instance Name | `nautilus-ec2`          |
| AMI           | `ami-0c101f26f147fa7fd` |
| Instance Type | `t2.micro`              |

---

# Terraform Configuration

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "nautilus_ec2" {
  ami           = "ami-0c101f26f147fa7fd"
  instance_type = "t2.micro"

  tags = {
    Name = "nautilus-ec2"
  }
}
```

---

# Commands Used

```bash
terraform init
terraform validate
terraform plan
terraform apply -auto-approve
```

---

# Key Learnings

* EC2 provides scalable virtual servers.
* AMI defines operating system templates.
* Terraform can fully automate server provisioning.

---

# Interview Questions

### What is an EC2 instance?

A virtual machine running in AWS cloud.

---

### What is an AMI?

Amazon Machine Image used to launch EC2 instances.

---

### Which Terraform resource creates EC2?

```hcl
aws_instance
```
