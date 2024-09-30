# AWS Infrastructure Project Using CloudFormation

This project contains AWS CloudFormation templates for deploying an AWS infrastructure setup, including VPC, EC2 instances, RDS, Network Load Balancer (NLB), and S3 services. The infrastructure is modularized into several CloudFormation stack templates for better organization and reusability.
![complete-architecture](Screenshot.png)


## Table of Contents

- [CloudFormation Stacks](#cloudformation-stacks)
- [Usage](#usage)
    -  [Running the Stack](#running-the-stack)
        - [Deploy the Main Template](#running-the-stack)
        - [Create the CloudFormation Stack](#running-the-stack)
        - [Specify Stack Details](#running-the-stack)
        - [Configure Stack Options](#running-the-stack)
        - [Review and Create](#running-the-stack)
        - [Monitor the Stack Creation](#running-the-stack)
        - [Access Outputs](#running-the-stack)
    -  [Prerequisites](#prerequisites)


## CloudFormation Stacks

```graphql
/question-1-cloudformation
├── cloudfront-plus-s3-stack.yml
├── cloudfront-stack.yml
├── ec2-stack.yml
├── networking-stack.yml
├── nlb-stack.yml
├── rds-stack.yml
├── s3-stack.yml
├── ssmhost.yml
├── template.yml
├── vpc-endpoints.yml
└── vpc-stack.yml
```

1. VPC Stack **(`vpc-stack.yml`)**

    This stack sets up a Virtual Private Cloud (VPC) with public and private subnets, an Internet Gateway, and NAT Gateways. It outputs references to created resources for use in other stacks.

2. RDS Stack **(`rds-stack.yml`)**

    This stack provisions a MariaDB RDS instance within the defined private subnets. It includes settings for backups, maintenance windows, and security group configuration.

3. NLB Stack **(`nlb-stack.yml`)**

    This stack creates a Network Load Balancer (NLB) to distribute incoming traffic across multiple targets. It defines a target group and listener configuration.

4. S3 Stack **(`s3-stack.yml`)**

    This stack creates an S3 bucket to store data. The bucket name is defined in the properties.

5. SSM Host Stack **(`ssmhost.yml`)**

    This stack provisions an EC2 instance with SSM Agent and necessary IAM roles for management and access. The instance runs in a public subnet.

6. VPC Endpoints Stack **(`vpc-endpoints.yml`)**

    This stack sets up interface VPC endpoints for AWS services (SSM, EC2, etc.) and a gateway endpoint for S3, ensuring private connectivity to AWS services from private subnets.

7. CloudFront Plus S3 Stack **(`cloudfront-plus-s3-stack.yml`)**

    This stack integrates CloudFront with the S3 bucket for optimized content delivery and caching. It outputs the CloudFront distribution details.

8. CloudFront Stack **(`cloudfront-stack.yml`)**

    This stack creates a standalone CloudFront distribution for serving static and dynamic content from various origins.

9. EC2 Stack **(`ec2-stack.yml`)**

    This stack provisions EC2 instances with specific configurations, security groups, and associated resources for application deployment.

10. Networking Stack **(`networking-stack.yml`)**

    This stack includes configurations for networking components such as security groups, route tables, and other network-related resources.

11. Template Stack **(`template.yml`)**

    This is the main entry point that orchestrates all other stacks, providing parameters and invoking the nested stacks.


## Usage

### Running the Stack

1. **Deploy the Main Template:**

   - Upload all your stack templates (e.g., vpc-stack.yml, ssmhost.yml, etc.) to an S3 bucket in your AWS account.
   - Make sure the S3 bucket is publicly accessible or configure your CloudFormation stack with the appropriate IAM roles for access.


2. **Create the CloudFormation Stack:**

   - Navigate to the AWS CloudFormation console.
   - Click on Create stack > With new resources (standard).
   - Choose Upload a template file or specify the S3 URL for the template.yml file.
   - Click Next.


3. **Specify Stack Details:**

   - Provide a stack name.
   - Fill in the required parameters, such as the S3 bucket URL where your templates are stored.


4. **Configure Stack Options (optional):**

   - Configure tags, permissions, and advanced options as needed.


5. **Review and Create:**

   - Review your stack configuration.
   - Click on Create stack to initiate the deployment.


6. **Monitor the Stack Creation:**

   - Monitor the stack creation process in the AWS CloudFormation console. You can view the status of each individual stack and its resources.


7. **Access Outputs:**

   - Once the stacks are created successfully, access the outputs of each stack for important resource identifiers like VPC ID, subnet IDs, and DNS names.


### Prerequisites

   - AWS account
   - AWS CLI configured with proper permissions

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

