
# AWS Cloud Architect Projects Udacity

*The listed projects were part of my AWS Cloud Architect Nanodegree and are displayed in derivated form due to possible copyright restrictions.*

*Form and requirements of my projects may differ from present projects. Udacity may vary projects and this repo is representing my findings at this point in time and may not be representative for future  AWS Cloud Architect projects. If you are currently enrolled into Udacity's AWS Cloud Architect Nanodegree please keep in mind that my findings can help you as a guide but copying these findings will go against Udacity's Honor Code.*


# Project 2: Design, Provision and Monito AWS Infrastructure at Scale

In this project, you will plan, design, provision, and monitor infrastructure in AWS using industry-standard and open source tools. You will practice the skills you have learned throughout the course to optimize infrastructure for cost and performance. You will also use Terraform to provision and configure AWS services in a global configuration.

**Task 1: Create AWS Architecture Schematics**

**Part 1**

You have been asked to plan and provision a cost-effective AWS infrastructure for a new social media application development project for 50,000 single-region users. The project requires the following AWS infrastructure and services. Please include your name and label all elements of the infrastructure on the diagram.

- Infrastructure in the following regions: us-east-1
- Users and Client machines
- One VPC
- Two Availability Zones
- Four Subnets (2 Public, 2 Private)
- A NAT Gateway
- A CloudFront distribution with an S3 bucket
- Web servers in the Public Subnets sized according to your usage estimates
- Application Servers in the Private Subnets sized according to your usage estimates
- DB Servers in the Private Subnets
- Web Servers Load Balanced and Autoscaled
- Application Servers Load Balanced and Autoscaled
- A Master DB in AZ1 with a read replica in AZ2
- Use LucidChart or a similar diagramming application to create your schematic. 
Export your schematic as a PDF and save as Udacity_Diagram_1.pdf.

**Solution:**

![alt text](https://github.com/mikethwolff/AWS-Cloud-Architect-Project-Design-Provision-and-Monitor-AWS-Infrastructure-at-Scale/blob/main/Design%2C%20Provision%20and%20Monito%20AWS%20Infrastructure%20at%20Scale/Udacity_Diagram_1.jpg)

**Task 2: Calculate Infrastructure Costs**

Use the AWS Pricing Calculator to estimate how much it will cost to run the services in your Part 1 diagram for one month.

- Target a monthly estimate between $8,000-$10,000.
- Be mindful of AWS regions when you are estimating costs.
- Export the estimate as a CSV file named Initial_Cost_Estimate.csv.

**Solution:**

Initial_Cost_Estimate.csv
```
Group hierarchy	Region	Service	Upfront	Monthly	First 12 months total	Currency	Configuration summary
My Estimate	US East (N. Virginia)	Amazon EC2	0	746.83	8961.96	USD	Operating system (Linux), Quantity (6), Pricing strategy (OnDemand), Storage amount (30 GB), Instance type (t3.xlarge)
My Estimate	US East (N. Virginia)	Amazon EC2	0	762.6	9151.2	USD	Operating system (Linux), Quantity (6), Pricing strategy (OnDemand), Storage amount (30 GB), Instance type (c5.xlarge)
My Estimate	US East (N. Virginia)	Application Load Balancer	0	191.63	2299.56	USD	Number of Application Load Balancers (1)
My Estimate	US East (N. Virginia)	S3 Standard	0	94.21	1130.52	USD	S3 Standard storage (4 TB per month)
My Estimate	US East (N. Virginia)	Data Transfer	0	0	0	USD	DT Inbound: All other regions (4 TB per month), DT Outbound: Amazon CloudFront (4 TB per month)
My Estimate	US East (N. Virginia)	Amazon Aurora PostgreSQL-Compatible DB	0	6,560.05	78,720.60	USD	Storage amount (4 TB), Quantity (2), Instance type (db.r6g.8xlarge), Pricing strategy (OnDemand), Additional backup storage (4 TB)
My Estimate	US East (N. Virginia)	Amazon Virtual Private Cloud (VPC)	0	434.34	5212.08	USD	Number of NAT Gateways (2)
My Estimate	US East (N. Virginia)	Amazon Route 53	0	938.5	11262	USD	Hosted Zones (2), Basic Checks Within AWS (100), Number of Elastic Network Interfaces (10)
							
Total:	9728.16		116737.92	USD	
							
Acknowledgement							
* AWS Pricing Calculator provides only an estimate of your AWS fees and doesn't include any taxes that might apply. Your actual fees depend on a variety of factors, including your actual usage of AWS services.							
```

Return to the AWS Pricing Calculator and reconfigure your estimates for the following scenarios:

Your budget has been reduced from $8,000-$10,000 to a maximum of $6,500. What services will you modify to meet this new budget? Export the updated costs in a CSV file named Reduced_Cost_Estimate.csv and write up a brief narrative of the changes you made in the CSV file below the cost estimate.

**Solution:**

Reduced_Cost_Estimate.csv
```
Group hierarchy	Region	Service	Upfront	Monthly	First 12 months total	Currency	Configuration summary
My Estimate	US East (N. Virginia)	Amazon EC2	0	316.56	3,798.72	USD	Operating system (Linux), Quantity (4), Pricing strategy (EC2 Instance Savings Plans 1 Year No Upfront), Storage amount (30 GB), Instance type (t3.xlarge)
My Estimate	US East (N. Virginia)	Amazon EC2	0	324.44	3,893.28	USD	Operating system (Linux), Quantity (4), Pricing strategy (EC2 Instance Savings Plans 1 Year No Upfront), Storage amount (30 GB), Instance type (c5.xlarge)
My Estimate	US East (N. Virginia)	Application Load Balancer	0	191.63	2299.56	USD	Number of Application Load Balancers (1)
My Estimate	US East (N. Virginia)	S3 Standard	0	94.21	1130.52	USD	S3 Standard storage (4 TB per month)
My Estimate	US East (N. Virginia)	Data Transfer	0	0	0	USD	DT Inbound: All other regions (4 TB per month), DT Outbound: Amazon CloudFront (4 TB per month)
My Estimate	US East (N. Virginia)	Amazon Aurora PostgreSQL-Compatible DB	0	4,469.04	53,628.48	USD	Storage amount (4 TB), Quantity (2), Instance type (db.r6g.8xlarge), Pricing strategy (Reserved 1yr No Upfront), Additional backup storage (4 TB)
My Estimate	US East (N. Virginia)	Amazon Virtual Private Cloud (VPC)	0	434.34	5212.08	USD	Number of NAT Gateways (2)
My Estimate	US East (N. Virginia)	Amazon Route 53	0	482.25	5,787	USD	Hosted Zones (2), Basic Checks Within AWS (100), Number of Elastic Network Interfaces (5)
							
Total:	6312.47		75,749.64	USD	
							
- Pricing strategy changed from on-demand to EC2 Instance Savings Plans 1 Year No Upfront on all servers				
- RDS pricing strategy changed from on-demand to Reserved 1yr No Upfront				
- Route 53 with reduced number of Elastic Network Interfaces	

Acknowledgement							
* AWS Pricing Calculator provides only an estimate of your AWS fees and doesn't include any taxes that might apply. Your actual fees depend on a variety of factors, including your actual usage of AWS services.							
```

Your budget has been increased to $20,000. What resources will you add and why?
Think about where to add redundancy and how to improve performance. Re-configure your estimate to a monthly invoice of $18K-20K. Export the updated costs to a CSV file named Increased_Cost Estimate.csv and write up a brief narrative of the changes you made in the CSV file below the cost estimate.

**Solution:**
Increased_Cost Estimate.csv
```
Group hierarchy	Region	Service	Upfront	Monthly	First 12 months total	Currency	Configuration summary
My Estimate	US East (N. Virginia)	Amazon EC2	0	3570.78	42849.36	USD	Operating system (Linux), Quantity (10), Pricing strategy (EC2 Instance Savings Plans 1 Year No Upfront), Storage amount (2 TB), Instance type (t3.2xlarge)
My Estimate	US East (N. Virginia)	Amazon EC2	0	4634.2	55610.4	USD	Operating system (Linux), Quantity (10), Pricing strategy (EC2 Instance Savings Plans 1 Year No Upfront), Storage amount (3 TB), Instance type (c5.2xlarge)
My Estimate	US East (N. Virginia)	Application Load Balancer	0	191.63	2299.56	USD	Number of Application Load Balancers (1)
My Estimate	US East (N. Virginia)	S3 Standard	0	94.21	1130.52	USD	S3 Standard storage (4 TB per month)
My Estimate	US East (N. Virginia)	Data Transfer	0	0	0	USD	DT Inbound: All other regions (4 TB per month), DT Outbound: Amazon CloudFront (4 TB per month)
My Estimate	US East (N. Virginia)	Amazon Aurora PostgreSQL-Compatible DB	0	8441.406	101296.87	USD	Storage amount (4 TB), Quantity (2), Instance type (db.r6g.16xlarge), Pricing strategy (Reserved 1yr No Upfront), Additional backup storage (4 TB)
My Estimate	US East (N. Virginia)	Amazon Virtual Private Cloud (VPC)	0	434.34	5212.08	USD	Number of NAT Gateways (2)
My Estimate	US East (N. Virginia)	Amazon Route 53	0	1851	22212	USD	Hosted Zones (2), Basic Checks Within AWS (100), Number of Elastic Network Interfaces (20)
							
Total:	19217.566	230610.79	USD	
							
- Increase number of virtual CPUs and amount of memory on EC2s				
- Route 53 increase of Number of Elastic Network Interfaces				
- RDS instance upgrade with increased number of CPU cores and amount of memory				
							
Acknowledgement							
* AWS Pricing Calculator provides only an estimate of your AWS fees and doesn't include any taxes that might apply. Your actual fees depend on a variety of factors, including your actual usage of AWS services.							
```

**Task 5: Use Terraform to Provision AWS Infrastructure**

**Part 1**

Download the starter code. In the main-terraform.tf file write the code to provision

- AWS as the cloud provider
- Use an existing VPC ID
- Use an existing public subnet
- 4 AWS t2.micro EC2 instances named Udacity T2
- 2 m4.large EC2 instances named Udacity M4
- Run Terraform.
- Take a screenshot of the 6 EC2 instances in the AWS console
- Use Terraform to delete the 2 m4.large instances
- Take an updated screenshot of the AWS console showing only the 4 t2.micro instances

**Solution:**

main-terraform.tf
```
# TODO: Designate a cloud provider, region, and credentials

provider "aws" {
access_key = "***"
secret_key = "***"
region = "us-east-1"
}

# TODO: provision 4 AWS t2.micro EC2 instances named Udacity T2

resource "aws_instance" "Udacity_T2" {
  count = "4"
  ami = "ami-087c17d1fe0178315"
  instance_type = "t2.micro"
  tags = {
    name = "Udacity_T2"
  }
}

# TODO: provision 2 m4.large EC2 instances named Udacity M4

resource "aws_instance" "Udacity_M4" {
  count = "2"
  ami = "ami-087c17d1fe0178315"
  instance_type = "m4.large"
  tags = {
    name = "Udacity_M4"
  }
}
```

![alt text](https://github.com/mikethwolff/AWS-Cloud-Architect-Project-Design-Provision-and-Monitor-AWS-Infrastructure-at-Scale/blob/main/Design%2C%20Provision%20and%20Monito%20AWS%20Infrastructure%20at%20Scale/Terraform_1_1.png)

![alt text](https://github.com/mikethwolff/AWS-Cloud-Architect-Project-Design-Provision-and-Monitor-AWS-Infrastructure-at-Scale/blob/main/Design%2C%20Provision%20and%20Monito%20AWS%20Infrastructure%20at%20Scale/Terraform_1_2.png)

**Part 2**

In the Exercise_2 folder, write the code to deploy an AWS Lambda Function using Terraform. Your code should include:
A lambda.py file, a main.tf file, outputs.tf file, variables.tf file

- Take a screenshot of the EC2 instances page
- Take a screenshot of the VPC page
- Take a screenshot of the CloudWatch log entry for the lambda function execution

**Solution:**

main.tf
```
#cloud provider 
provider "aws" {
access_key = "***"
secret_key = "***"
region = "us-east-1"
}


# lambda role
resource "aws_iam_role" "lambda_exec_role" {
  name = "lambda_exec_role"
  assume_role_policy = <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": "sts:AssumeRole",
      "Principal": {
        "Service": "lambda.amazonaws.com"
      },
      "Effect": "Allow",
      "Sid": ""
    }
  ]
}
EOF
}


# cloudwatch
resource "aws_cloudwatch_log_group" "lambda_log_group" {
  name              = "/aws/lambda/${var.lambda_name}"
  retention_in_days = 7
}

resource "aws_iam_policy" "lambda_logs_policy" {
  name        = "lambda_logs_policy"
  path        = "/"
  policy = <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents"
      ],
      "Resource": "arn:aws:logs:*:*:*",
      "Effect": "Allow"
    }
  ]
}
EOF
}


#data
data "archive_file" "lambda_zip" {
    type = "zip"
    source_file = "greet_lambda.py"
    output_path = var.lambda_output_path
}


#policy
resource "aws_iam_role_policy_attachment" "lambda_logs_policy" {
  role       = aws_iam_role.lambda_exec_role.name
  policy_arn = aws_iam_policy.lambda_logs_policy.arn
}


# lambda function
resource "aws_lambda_function" "geeting_lambda" {
  function_name = var.lambda_name
  filename = data.archive_file.lambda_zip.output_path
  source_code_hash = data.archive_file.lambda_zip.output_base64sha256
  handler = "greet_lambda.lambda_handler"
  runtime = "python3.8"
  role = aws_iam_role.lambda_exec_role.arn

  environment{
      variables = {
          greeting = "Wassup Udacity!"
      }
  }

  depends_on = [aws_iam_role_policy_attachment.lambda_logs_policy, aws_cloudwatch_log_group.lambda_log_group]
}
```

greet_lambda.py
```
import os

def lambda_handler(event, context):
    return "{} from Lambda!".format(os.environ['greeting'])
```

variables.tf
```
# TODO: Define the variable for aws_region

variable "aws_region" {
  default = "us-east-1"
}

variable "lambda_name" {
  default = "greet_lambda"
}

variable "lambda_output_path" {
  default = "output.zip"
}
```

outputs.tf
```
# TODO: Define the output variable for the lambda function.

output "lambda_function_arn" {
  value = "${aws_lambda_function.geeting_lambda.arn}"
}
```

![alt text](https://github.com/mikethwolff/AWS-Cloud-Architect-Project-Design-Provision-and-Monitor-AWS-Infrastructure-at-Scale/blob/main/Design%2C%20Provision%20and%20Monito%20AWS%20Infrastructure%20at%20Scale/Terraform_2_1.png)

![alt text](https://github.com/mikethwolff/AWS-Cloud-Architect-Project-Design-Provision-and-Monitor-AWS-Infrastructure-at-Scale/blob/main/Design%2C%20Provision%20and%20Monito%20AWS%20Infrastructure%20at%20Scale/Terraform_2_2.png)

![alt text](https://github.com/mikethwolff/AWS-Cloud-Architect-Project-Design-Provision-and-Monitor-AWS-Infrastructure-at-Scale/blob/main/Design%2C%20Provision%20and%20Monito%20AWS%20Infrastructure%20at%20Scale/Terraform_2_3.png)

**Task 6: Destroy the Infrastructure using Terraform and prepare for submission**

- Destroy all running provisioned infrastructure using Terraform so as not to incur unwanted charges
- Take a screenshot of the EC2 instances page
- Upload Terraform files, screenshots, schematics and CSV files to your GitHub repo

![Terraform_destroyed](https://github.com/mikethwolff/AWS-Cloud-Architect-Project-Design-Provision-and-Monitor-AWS-Infrastructure-at-Scale/blob/main/Design%2C%20Provision%20and%20Monito%20AWS%20Infrastructure%20at%20Scale/Terraform_destroyed.png)

