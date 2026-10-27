# Terraform-Notes
Terraform notes &amp; Certification
Once Terraform installed in Laptop. Open the Terraform CLI or Powershell 
> terraform version
> mkdir C:\terraform-practice
> cd C:\terraform-practice
> notepad .\main.tf
**Paste the configuration in notepad.**
terraform {
  required_providers {
    local = {
      source  = "hashicorp/local"
      version = "~> 2.5"
    }
  }
}

resource "local_file" "hello" {
  filename = "${path.module}/hello.txt"
  content  = "Hello from Terraform"
}
**PowerShell, run these commands one at a time**
terraform init
terraform fmt
terraform validate
terraform plan
Task 2 
