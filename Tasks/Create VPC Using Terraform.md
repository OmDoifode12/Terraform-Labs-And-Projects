# Day 02 – Create VPC Using Terraform

---

## Task Overview

The Nautilus DevOps team is beginning their AWS cloud migration journey by provisioning networking resources using Terraform. As part of the infrastructure setup, they need to create a Virtual Private Cloud (VPC) to host AWS services securely.

For this task, create a VPC named `xfusion-vpc` in the `us-east-1` region using Terraform.

---

# Objective

| Property          | Value         |
| ----------------- | ------------- |
| Resource Type     | VPC           |
| Name              | `xfusion-vpc` |
| Region            | `us-east-1`   |
| Provisioning Tool | Terraform     |

---

# Step-by-Step Implementation

## Step 1: Navigate to Terraform Directory

```bash
cd /home/bob/terraform
```

---

## Step 2: Create main.tf

```bash
touch main.tf
```

---

## Step 3: Add Terraform Configuration

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

---

## Step 4: Initialize Terraform

```bash
terraform init
```

---

## Step 5: Validate Configuration

```bash
terraform validate
```

---

## Step 6: Preview Infrastructure

```bash
terraform plan
```

---

## Step 7: Apply Configuration

```bash
terraform apply -auto-approve
```

---

# Key Learnings

* VPC is the foundation of AWS networking.
* Terraform automates infrastructure provisioning.
* CIDR blocks define private network ranges.
* Tags help identify cloud resources.

---

# Interview Questions

### What is a VPC?

A VPC is a logically isolated virtual network inside AWS.

---

### What does CIDR block mean?

CIDR defines the IP address range for the network.

---

### Which Terraform resource creates a VPC?

```hcl
aws_vpc
```
