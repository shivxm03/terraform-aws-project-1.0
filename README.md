# Terraform AWS Infrastructure Deployment

This Terraform project sets up a basic infrastructure on AWS including VPC, subnets, security groups, S3 bucket, EC2 instances, and an Application Load Balancer (ALB).

## Infrastructure Components

### VPC (Virtual Private Cloud)
- Creates a custom VPC with specified CIDR block.
- Defines two public subnets across different availability zones (`ca-central-1a` and `ca-central-1b`).
- Associates an internet gateway to allow outbound internet traffic.

### Security Groups
- Defines a security group (`websg`) allowing inbound traffic on port 80 (HTTP) and port 22 (SSH) from anywhere.
- Allows all outbound traffic.

### S3 Bucket
- Creates an S3 bucket (`myterraforminfraproject`) with public read access.

### EC2 Instances
- Launches two t2.micro EC2 instances (`Hello1` and `Hello2`) in the defined subnets.
- Associates the `websg` security group and IAM instance profile with EC2 instances.
- Uses user data scripts to install Apache web server and display instance metadata on the default web page.

### Application Load Balancer (ALB)
- Sets up an ALB (`myalb`) as an internet-facing application load balancer.
- Configures listeners and target groups (`myTG`) to route traffic to the EC2 instances.

## Usage

### Prerequisites
- Install [Terraform](https://www.terraform.io/downloads.html).
- Configure AWS credentials using AWS CLI (`aws configure`) or environment variables.

### Deployment Steps
1. Connect with IAM token and credentials.

2. Initialize Terraform and apply the configuration.

```bash
terraform init
terraform apply
```
3. Review the planned actions and confirm by typing yes.

4. After successful deployment, the public DNS of the ALB (loadbalancerdns) will be displayed as an output.

5. Access the ALB DNS endpoint in a web browser to see the deployed web servers.

Cleanup
To tear down the infrastructure created by Terraform, run:

```bash
terraform destroy
```
