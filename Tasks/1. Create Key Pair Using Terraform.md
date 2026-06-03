# Day 01 – Create Key Pair Using Terraform

---

## Task Overview

When provisioning infrastructure in AWS, secure access to EC2 instances is essential. AWS Key Pairs provide a secure mechanism for authenticating SSH connections to Linux instances. As part of their cloud migration strategy, the Nautilus DevOps team is automating infrastructure provisioning using Terraform.

For this task, create an AWS Key Pair named `nautilus-kp` using Terraform.

---

## Objective

Create an AWS Key Pair with the following requirements:

| Property          | Value         |
| ----------------- | ------------- |
| Key Pair Name     | `nautilus-kp` |
| Key Type          | RSA           |
| Provisioning Tool | Terraform     |
| Region            | us-east-1     |

---

# Understanding AWS Key Pairs

AWS Key Pairs consist of:

* Public Key (stored in AWS)
* Private Key (stored securely by the user)

The private key is used to SSH into EC2 instances.

Benefits:

* Passwordless authentication
* Improved security
* Industry standard for Linux servers

---

# Step-by-Step Implementation

## Step 1: Navigate to Terraform Directory

```bash
cd /home/bob/terraform
```

### Explanation

This is the working directory where Terraform configuration files are stored.

---

## Step 2: Generate RSA Key Pair

```bash
ssh-keygen -t rsa -f nautilus-kp
```

Press Enter when prompted.

### Explanation

This command creates:

| File            | Purpose     |
| --------------- | ----------- |
| nautilus-kp     | Private Key |
| nautilus-kp.pub | Public Key  |

Terraform uploads the public key to AWS.

---

## Step 3: Create main.tf

```bash
touch main.tf
```

### Explanation

Terraform configurations are stored inside `.tf` files.

---

## Step 4: Add Terraform Configuration

```hcl
resource "aws_key_pair" "nautilus_kp" {
  key_name   = "nautilus-kp"
  public_key = file("nautilus-kp.pub")
}
```

### Explanation

| Parameter    | Description                         |
| ------------ | ----------------------------------- |
| aws_key_pair | Terraform resource for AWS Key Pair |
| key_name     | Name of the AWS Key Pair            |
| public_key   | Uploads local RSA public key        |

---

## Step 5: Initialize Terraform

```bash
terraform init
```

### Explanation

Downloads and initializes required Terraform providers.

---

## Step 6: Validate Configuration

```bash
terraform validate
```

### Explanation

Checks Terraform syntax and configuration correctness.

---

## Step 7: Preview Changes

```bash
terraform plan
```

### Explanation

Shows resources Terraform will create before applying changes.

---

## Step 8: Apply Configuration

```bash
terraform apply -auto-approve
```

### Explanation

Creates the AWS Key Pair automatically.

---

## Step 9: Verify Key Pair

```bash
aws ec2 describe-key-pairs \
--key-names nautilus-kp \
--region us-east-1
```

### Explanation

Verifies that the key pair exists in AWS.

---

# Terraform Workflow Used

## 1. Write Configuration

Create infrastructure definitions in `.tf` files.

```bash
main.tf
```

---

## 2. Initialize

```bash
terraform init
```

Downloads providers and initializes Terraform.

---

## 3. Validate

```bash
terraform validate
```

Checks configuration syntax.

---

## 4. Plan

```bash
terraform plan
```

Previews infrastructure changes.

---

## 5. Apply

```bash
terraform apply
```

Creates infrastructure resources.

---

## 6. Verify

Confirm resources were created successfully.

---

## 7. Destroy (Optional)

```bash
terraform destroy
```

Removes provisioned infrastructure.

---

# Best Practices

* Never commit private keys to GitHub.
* Store private keys securely.
* Use IAM roles whenever possible.
* Rotate SSH keys periodically.
* Use Terraform state management properly.
* Follow least-privilege security principles.

---

# Key Learnings

* Terraform can automate AWS Key Pair creation.
* AWS stores only the public key.
* RSA is commonly used for SSH authentication.
* Infrastructure can be managed as code.
* Terraform provides repeatable and consistent deployments.

---

# Interview Questions & Answers

### 1. What is an AWS Key Pair?

An AWS Key Pair is a set of public and private keys used for securely accessing EC2 instances.

---

### 2. Why is the private key important?

The private key is required to authenticate SSH connections to EC2 instances.

---

### 3. Does AWS store the private key?

No. AWS stores only the public key.

---

### 4. What Terraform resource is used to create a Key Pair?

```hcl
aws_key_pair
```

---

### 5. What does `terraform init` do?

It initializes the working directory and downloads required providers.

---

### 6. What is the purpose of `terraform plan`?

It previews infrastructure changes before deployment.

---

### 7. What is Infrastructure as Code (IaC)?

Managing and provisioning infrastructure through code rather than manual processes.

---

### 8. What is the difference between `terraform apply` and `terraform destroy`?

| Command           | Purpose                   |
| ----------------- | ------------------------- |
| terraform apply   | Creates/updates resources |
| terraform destroy | Removes resources         |

---

### 9. Why should private keys never be uploaded to GitHub?

Anyone with the private key can gain unauthorized access to servers.

---

### 10. What are the advantages of Terraform?

* Automation
* Consistency
* Repeatability
* Version Control
* Multi-cloud Support
