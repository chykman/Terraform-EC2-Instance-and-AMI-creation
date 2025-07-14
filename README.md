# ✅ Terraform: EC2 Instance and AMI Creation Project

This project demonstrates how to:
- Provision an EC2 instance with Terraform
- Create a custom AMI from that instance
- Modify infrastructure
- Clean up resources
- Verify AWS CLI configuration
- Document observations and lessons learned

---

## 📌 Prerequisites Verification

### 🔧 AWS CLI Installation
AWS CLI must be installed to interact with AWS from the terminal.

📷 **Screenshot: AWS CLI installed**  
![AWS CLI Installation](https://github.com/user-attachments/assets/aws-cli-installed-screenshot.png)

### ✅ AWS Authentication

Run the following command to confirm you are authenticated:

```bash
aws sts get-caller-identity
```

📷 **Screenshot: Authenticated AWS Identity**  
![STS Get Caller Identity](https://github.com/user-attachments/assets/aws-sts-get-caller-identity.png)

---

## 📁 Project Setup

### 1. Create Project Directory

```bash
mkdir terraform-ec2-ami
cd terraform-ec2-ami
```

📷 **Screenshot**  
![Project Directory Created](https://github.com/user-attachments/assets/b021950b-7f26-44d0-84e1-17b2b87972ec)

---

### 2. Create Terraform Configuration File `main.tf`

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example_instance" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  key_name      = "your-key-pair"
  # subnet_id and security_group may be added here
}

resource "aws_ami" "example_ami" {
  name        = "example-ami"
  description = "Example AMI created with Terraform"
  instance_id = aws_instance.example_instance.id
}
```

📷 **Screenshot**  
![main.tf file](https://github.com/user-attachments/assets/9750d55a-5fc7-429d-ab6f-041386bf939d)

---

## 🔄 Terraform Workflow

### 3. Initialize Terraform

```bash
terraform init
```

📷 **Screenshot**  
![Terraform Init](https://github.com/user-attachments/assets/5f1e6a21-f6eb-4e63-aa04-7cacfa2dec56)

---

### 4. Validate the Configuration

```bash
terraform validate
```

📷 **Screenshot**  
![Terraform Validate](https://github.com/user-attachments/assets/terraform-validate-screenshot.png)

---

### 5. Apply Configuration

```bash
terraform apply
```

📷 **Screenshot**  
![Terraform Apply](https://github.com/user-attachments/assets/3953ea85-b252-4f21-aaec-ebbb521fb520)

📷 **AWS Console: EC2 Running**  
![EC2 Instance](https://github.com/user-attachments/assets/f4d4b775-59f8-4e71-a719-59811578a73e)

---

## 🔁 Modify the Infrastructure

### 6. Change Instance Type (e.g., `t2.micro` → `t2.small`)

📷 **Initial Type**  
![Old Type](https://github.com/user-attachments/assets/45dcd3a3-818a-4abd-89e1-f8fcb096d02f)

📷 **Modified Configuration**  
![Modified main.tf](https://github.com/user-attachments/assets/5b3e609d-6d38-4dab-a5bd-bed0e4f6ad91)

📷 **Terraform Apply Updated**  
![Apply Modified](https://github.com/user-attachments/assets/92166d4c-925c-4039-9acd-f45670b8d02f)

📷 **AWS Console: Confirmed Type Change**  
![Modified Instance](https://github.com/user-attachments/assets/bd905f47-2f9e-4145-a136-9370fd96cb2f)

---

## 🧹 Clean Up Resources

### 7. Destroy Infrastructure

```bash
terraform destroy
```

📷 **Terraform Destroy Execution**  
![Destroy Command](https://github.com/user-attachments/assets/d04c7c56-e8c8-4b52-b2f4-7fe797009d47)

📷 **Destroy Confirmed**  
![Destroy Output](https://github.com/user-attachments/assets/221e6284-5b18-4648-ac26-3c642c19a476)

📷 **AWS Console: Instance Terminated**  
![EC2 Terminated](https://github.com/user-attachments/assets/6be9bd20-cb8c-4204-b5b7-25169a8ded27)

---

## 📖 Observations & Lessons Learned

- **Terraform Validate** is helpful to catch errors early before provisioning resources.
- When using a custom AMI resource, ensure the instance is in a proper state before imaging.
- **Key pairs** must already exist in AWS for EC2 creation to succeed.
- Updating the instance type triggers a **recreation** of the instance.
- **Terraform destroy** effectively removes all provisioned resources but requires careful use to avoid accidental deletion.

---
