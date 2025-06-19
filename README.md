# Jenkins HA Setup on AWS (Terraform + Ansible + Packer)

Setting up a Highly Available Jenkins (HA) Environment on AWS using Terraform, Ansible, and Packer

* For this Jenkins HA project, I have used the following DevOps Tools

    *GitHub:* Repository to store IaC
    *Packer:* To build Jenkins Controller and agent AMIs
    *Ansible:* To configure Jenkins controller and agent during the AMI building process
    *Terraform:* To provision AWS resources
    *Python Boto3:* To retrieve SSH public key from AWS parameter store.

* Following are the AWS services used.

    *IAM:* To create IAM Role/Instance Profile for Jenkins Controller and Agent Nodes.
    *EFS:* To store Jenkins data
    *AWS Parameter Store:* To store SSH private and public keys as secrets to configure agents.
    *Autoscaling Group:* To deploy the Jenkins controller
    *Application Load Balancer:* To have a static DNS endpoint for the Jenkins controller instance running in the autoscaling group.

## Prerequisite
o deploy this setup, you need to ensure that the following components are installed and properly configured on your workstation (laptop) or the server that you use for development.

Hashicorp Packer
Terraform
Ansible
AWS CLI is configured with default region as us-west-2 and AWS credentials that have admin access to the AWS account.
We will be using the default VPC in the us-west-2 (Oregon) region. There will be four default subnets. We will be using three subnets from the following three availability zones:

us-west-2a
us-west-2b
us-west-2c
Ensure you have an existing key pair in your AWS account for the Oregon region. We will use it with instances to enable SSH access.