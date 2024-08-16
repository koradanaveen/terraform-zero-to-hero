# MIGRATION TO TERRAFORM & DRIFT DETECTION

https://youtu.be/-4IMy5ihiiU

Migration of aws cloud formation template or azure resource manager template to terraform scripts here:
-> Here first need to write main.tf file with provider block, import block (need to write instance id of the resource which we want to import from CFT) 
import {
  id = "instance-id"

  to = aws_instance.example
}

terraform init -> initialising terraform
terraform plan -generate-config-out=generate_resource.tf -> it will generate a generate_resource.tf file having the instance details
after the above step we need to place resource details in main.tf file 
terraform plan -> if will try to create the new instance as we are not having statefile to check that for statefile to import we need to run below command
terraform import aws_instance.example <instance-id> -> to import the resource details with statefile 

If any changes were done manually to infra then we can identify issue using below ways:
terraform refresh as cron -> to refresh the stateFile to find any change in infrastructure
using audit logs or lambda notifier to alert the changes

