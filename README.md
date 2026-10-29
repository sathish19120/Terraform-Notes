# Terraform-Notes Terraform notes & Certification #
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
## Task 2 change the variable from PowerShell
> terraform plan -var="message=Learning Terraform variables"
> terraform apply -var="message=Learning Terraform variables"
> Get-Content .\hello.txt
> Learning Terraform variables
## Task 3 save variable values in terraform.tfvars
> notepad .\terraform.tfvars
> message = "Learning Terraform variables"
> run the commands
> Terraform init
> Terraform fmt
> Terraform validate
> Terraform plan
# Task 4 change the value in terraform.tfvars
> notepad .\terraform.tfvars
> Message = " I am preparing the Terraform Associate"
> save the file
> Terraform plan
> Terraform apply
# Task 5 organize your Terraform files
> notepad .\main.tf
> terraform {
  required_providers {
    local = {
      source  = "hashicorp/local"
      version = "~> 2.5"
    }
  }
}

resource "local_file" "hello" {
  filename = "${path.module}/hello.txt"
  content  = var.message
}
> Create variables.tf
> notepad .\variables.tf
> variable "message" {
  description = "Text to write into hello.txt"
  type        = string
  default     = "Hello from Terraform V2"
}
> notepad .\outputs.tf
> output "file_path" {
  description = "Path of the file Terraform manages"
  value       = local_file.hello.filename
}
> terraform fmt
terraform validate
terraform plan
> Remember the purpose
**File	Purpose**
main.tf	------------------Provider requirements and resources
variables.tf	------------Input variable declarations
terraform.tfvars---------	Values for those variables
outputs.tf	--------------Values Terraform displays
## Task 6 : implicit dependencies ##
**Note** : Concept: When one resource references another, Terraform automatically understands the dependency.
> Edit main.tf
> notepad .\main.tf
> resource "local_file" "notes" {
  filename = "${path.module}/notes.txt"
  content  = "My first Terraform file is: ${local_file.hello.filename}"
}
> save and close
> local_file.hello.filename
> terraform fmt
terraform validate
terraform plan
> terraform apply
> yes
> Get-Content .\notes.txt
> output : My first Terraform file is: ./hello.txt
## Task 7 : create multiple files using count ##
> We’ll create three new files while keeping your existing resources.
> open main.tf
> notepad .\main.tf
> resource "local_file" "practice" {
  count = 3

  filename = "${path.module}/practice-${count.index + 1}.txt"
  content  = "This is practice file ${count.index + 1}"
}
>save and close
>Understand the code
count.index starts at 0. Adding 1 makes the filenames start at 1.
Resource address	Created file
local_file.practice[0]	practice-1.txt
local_file.practice[1]	practice-2.txt
local_file.practice[2]	practice-3.txt
>terraform fmt
terraform validate
terraform plan
>terraform apply
>Get-ChildItem .\practice-*.txt
Get-Content .\practice-1.txt
terraform state list
>
>
