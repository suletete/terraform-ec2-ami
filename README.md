# Mini Project - Terraform EC2 Instance and AMI Creation

In this mini project, you will use Terraform to automate the creation of an EC2 instance on AWS and then create an Amazon Machine Image (AMI) from that instance.

---

## 🧠 Objectives

- Learn how to write basic Terraform configuration files.
- Automate the creation of an EC2 instance on AWS using Terraform.
- Automate the creation of an AMI from an existing EC2 instance on AWS using Terraform.

---

## ✅ Prerequisites

Ensure the following are completed before starting this project:

- You have an **AWS Account**.
- The **AWS CLI** is installed and configured locally.
- **Terraform** is installed on your computer.

> 💡 Refer to the respective official guides for:
> - [Creating an AWS account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
> - [Installing and configuring AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
> - [Installing Terraform](https://developer.hashicorp.com/terraform/downloads)

---

## 📝 Tasks Outline

1. Confirm the Prerequisites
2. Write the Terraform Script
3. Execute the Terraform Script
    - `terraform init`
    - `terraform validate`
    - `terraform plan`
    - `terraform apply`
4. Confirm Resources on AWS
5. Clean up using `terraform destroy`

---

## 🚀 Project Tasks

### Task 1 - Confirm the Prerequisites

Run the following commands on your terminal:

- Confirm AWS CLI is installed:
  ```bash
  aws --version


- Confirm AWS CLI is configured:
  ```bash
  aws configure list
  ```

- Confirm authentication with AWS:
  ```bash
  aws sts get-caller-identity
  ```

- Confirm Terraform is installed:
  ```bash
  terraform --version
  ```

---

### Task 2 - Develop the Terraform Script

1. Create a directory and navigate into it:

   ```bash
   mkdir terraform-ec2-ami
   cd terraform-ec2-ami
   ```

2. Create a Terraform config file:

   ```bash
   nano main.tf
   ```

3. Add the following code to `main.tf`:

   ```hcl
   provider "aws" {
     region = "us-east-1"  # Change to your preferred AWS region
   }

   resource "aws_instance" "my_ec2_spec" {
     ami           = "ami-0c55b159cbfafe1f0"  # Replace with a valid AMI ID for your region
     instance_type = "t2.micro"

     tags = {
       Name = "Terraform-created-EC2-Instance"
     }
   }

   resource "aws_ami" "my_ec2_spec_ami" {
     name               = "my-ec2-ami"
     description        = "My AMI created from my EC2 Instance with Terraform script"
     source_instance_id = aws_instance.my_ec2_spec.id
   }
   ```

---

### 📄 Script Explanation

#### Provider Block

- `provider "aws"` tells Terraform to use AWS as the provider.
- `region = "us-east-1"` specifies the AWS region.

#### EC2 Instance

- `resource "aws_instance"` creates an EC2 instance.
- `ami` is the AMI ID used to launch the instance.
- `instance_type` defines the instance type.
- `tags` help with resource identification.

#### AMI Creation

- `resource "aws_ami"` creates an AMI from the EC2 instance.
- `source_instance_id` references the EC2 instance created above.

---

### Task 3 - Execute the Terraform Script

Run the following commands:

1. Initialize the project:
   ```bash
   terraform init
   ```

2. Validate the script:
   ```bash
   terraform validate
   ```

3. View the execution plan:
   ```bash
   terraform plan
   ```

4. Apply the configuration:
   ```bash
   terraform apply
   ```

---

### Task 4 - Confirm Resources

- Go to the **AWS Console** → EC2 Dashboard
- Check for:
  - The EC2 Instance
  - The newly created AMI

---

### Task 5 - Clean Up

To delete all created resources:

```bash
terraform destroy
```

---

## 🧾 Documentation

### Observations

- [Your notes about what worked as expected]

### Challenges Faced

- [Any issues encountered and how you resolved them]

---

**End of Project**
```

Let me know if you'd like this exported as a `.md` file or need help with any specific part of the script!
