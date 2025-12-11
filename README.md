
# AWS Budget Accelerator

![Opstree Documentation](./images/opstree1.png)

[Opstree Solutions](https://opstree.github.io/)

## Overview

The AWS Budget Accelerator is a Python project designed to simplify the process of creating AWS Budgets and Budget Alarms for your AWS resources. AWS Budgets enable you to set spending and usage limits for your AWS services, and with this project, you can quickly configure and deploy AWS Budgets and corresponding alarms.

## AWS Budget Architecture

AWS Budget Architecture provides a framework for effectively managing and visualizing cost and usage data, allowing users to set budget limits, track actual expenses, and receive notifications for forecasted and actual budget breaches. The architecture leverages AWS Budgets and SNS notifications to enable proactive cost management and financial control within AWS environments.

![Budget Architecture](./images/architecture.png)


## Budgets Supported Include

| **Budget Type**                          | **Description**                                   | **Supported** |
|----------------------------------------|---------------------------------------------------|--------------|
| `Whole Account [Actual and Forecasted]`                        | Budget alerting for the entire AWS account on both Actual and Forecasted metrics               | Yes           |
| `Service Basis [Actual and Forecasted]`                        | Budget based on a specific services on both Actual and Forecasted metrics                    | Yes          | 
| `Tag Basis [Actual and Forecasted]`                        | Budget based on a specific tags along with specific services on both Actual and Forecasted metrics                    | Yes          | 
| `Savings Plans Usage`     | Budget alerting on utilization of Savings Plans      | Will be supported soon          |
| `Reserved Instances Usage` | Budget alerting on utilization of Reserved Instances | Yes   |
| `Custom Notification`     | Slack , Teams , Gchat Support     | Will be supported soon            |
| `Multiple Thresholds on Severity level` | Budget alerting on multiple severity levels like CRITICAL,WARNING,INFO etc | Will be supported soon   |
| `Custom Action on Threshold breach` | Taking action provided by user when specific threshold crossed  | No |

## Structure

The project structure is organized as follows:
```yaml
.
├── config
│   └── aws_budget_config_sample.yml
├── Dockerfile
├── images
│   ├── architecture.png
│   └── opstree1.png
├── LICENSE
├── Makefile
├── README.md
├── requirements.txt
├── scripts
│   ├── aws_budget_alerting.py
│   ├── aws_budget_factory.py
│   └── aws_budget_logger.py

```

- **scripts:** Contains the Python scripts for budget management.
- **config:** Holds the configuration files, such as `aws_budget_config_sample.yml`.

## Prerequisites

Before you begin using the AWS Budget Accelerator, ensure you have the following prerequisites in place:

- An AWS account with administrative privileges.
- AWS CLI installed and configured with appropriate IAM credentials.
- Python installed on your local machine.

**Note for Account Management:**
Only the AWS account root user can edit certain sections on the Account page. If you don't see the Edit option, switch to the root user.



## Inputs
The below outlines the current parameters and defaults.
### Python Configuration Variables
The below outlines the current parameters and defaults for the Python configuration file.
| **Variable Name**         | **Variable Type** | **Description**                                           | **Default Value**    | **Required** | 
|---------------------------|-------------------|-----------------------------------------------------------|----------------------|--------------|
| `aws_region`              | String            | The AWS region where the budget will be applied           | `us-east-1`          | Yes          |
| `aws_profile`             | String            | AWS CLI named profile for authentication                   | `Default`            | Yes          |
| `account_id`              | String            | AWS Account ID                                            | `Default`            | Yes          |
| `budget_name`             | String            | Name of the AWS Budget                                    | `MyBudget`           | Yes          |
| `budget_type`             | String            | Types of the AWS Budget (COST,RI_UTILIZATION etc)                                    | `COST`           | Yes          |
| `limit_amount`            | Number            | The specified budget limit amount (if applicable)         | ""                   | Yes          |
| `limit_unit`              | String            | Unit for the budget limit (default is USD)                | `USD`                | No           |
| `comparison_operator`     | String            | Operator for budget condition evaluation: LESS_THAN, EQUAL_TO, or GREATER_THAN | `GREATER_THAN` | No |
| `threshold`               | String            | Threshold value for notification triggering               | `100`                | No           |
| `threshold_type`          | String            | Type of threshold: PERCENTAGE or ABSOLUTE_VALUE           | `PERCENTAGE`         | No           |
| `notification_type`       | String            | Type of budget value to notify on: ACTUAL or FORECASTED   | `FORECASTED`         | Yes          |
|`recreate_budget_if_needed`| Boolean         | If True, it will delete existing same budget if exists and then will create a fresh budget. If False , then it will skip creating budget alert in case same budget exists in account| `True` | No


### Additional Budget Configuration

This table outlines additional parameters and defaults for configuring the AWS Budget:

| **Parameter Name**          | **Type**          | **Description**                                           | **Default Value**    | **Required** | 
|-----------------------------|-------------------|-----------------------------------------------------------|----------------------|--------------|
| `IncludeTax`                | Boolean           | Include tax in budget calculation                          | `True`               | No           |
| `IncludeSubscription`       | Boolean           | Include subscription costs in budget calculation           | `False`              | No           |
| `UseBlended`                | Boolean           | Use blended costs in budget calculation                    | `False`              | No           |
| `IncludeRefund`             | Boolean           | Include refunds in budget calculation                      | `False`              | No           |
| `IncludeCredit`             | Boolean           | Include credits in budget calculation                      | `False`              | No           |
| `IncludeUpfront`            | Boolean           | Include upfront costs in budget calculation                | `False`              | No           |
| `IncludeRecurring`          | Boolean           | Include recurring costs in budget calculation              | `False`              | No           |
| `IncludeOtherSubscription`  | Boolean           | Include other subscription costs in budget calculation     | `False`              | No           |
| `IncludeSupport`            | Boolean           | Include support costs in budget calculation                | `False`              | No           |
| `IncludeDiscount`           | Boolean           | Include discounts in budget calculation                    | `False`              | No           |
| `UseAmortized`              | Boolean           | Use amortized costs in budget calculation                  | `False`              | No           |



## Service Listing

This AWS Service Table gives you the service alias for adding directly in .yml file

| Service Alias        | AWS SERVICE                                 |
|-----------------|--------------------------------------------------|
| **EC2**         | Amazon Elastic Compute Cloud - Compute           |
| **ECR**         | Amazon EC2 Container Registry (ECR)              |
| **SQS**         | Amazon Simple Queue Service                      |
| **Tax**         | Tax                                              |
| **Athena**      | Amazon Athena                                    |
| **SES**         | Amazon Simple Email Service                      |
| **SNS**         | Amazon Simple Notification Service               |
| **VPC**         | Amazon Virtual Private Cloud                     |
| **WAF**         | AWS WAF                                          |
| **ECS**         | Amazon EC2 Container Service                     |
| **EKS**         | Amazon Elastic Container Service for Kubernetes  |
| **EBS**         | Amazon Elastic Block Store                       |
| **CloudFront**  | Amazon CloudFront                                |
| **CloudTrail**  | AWS CloudTrail                                   |
| **CloudWatch**  | Amazon CloudWatch                                |
| **Cognito**     | Amazon Cognito                                   |
| **Config**      | AWS Config                                       |
| **DynamoDB**    | Amazon DynamoDB                                  |
| **DMS**         | AWS Database Migration Service                   |
| **ElastiCache** | Amazon ElastiCache                               |
| **Elasticsearch** | Amazon Elasticsearch Service                   |
| **ELB**         | Amazon Elastic Load Balancing                    |
| **APIGateway**  | Amazon API Gateway                               |
| **Glue**        | AWS Glue                                         |
| **Kafka**       | Managed Streaming for Apache Kafka               |
| **KMS**         | AWS Key Management Service                       |
| **Kinesis**     | Amazon Kinesis                                   |
| **Lambda**      | AWS Lambda                                       |
| **Lex**         | Amazon Lex                                       |
| **Matillion**   | Matillion ETL for Amazon Redshift                |
| **Pinpoint**    | AWS Pinpoint                                     |
| **Polly**       | Amazon Polly                                     |
| **Rekognition** | Amazon Rekognition                               |
| **RDS**         | Amazon Relational Database Service               |
| **Redshift**    | Amazon Redshift                                  |
| **S3**          | Amazon Simple Storage Service                    |
| **SFTP**        | AWS Transfer for SFTP                            |
| **Route53**     | Amazon Route 53                                  |
| **SageMaker**   | Amazon SageMaker                                 |
| **SecretsManager** | AWS Secrets Manager                            |
| **XRay**        | AWS X-Ray                                        |

## Service Listing for Reserved Instances (RI) Utilization Budget Alerting

The following AWS services are supported specifically for Reserved Instances (RI) utilization budget alerting. Use these service aliases when configuring your .yml file for RI utilization budget alerts:

| Service Alias        | AWS SERVICE                                 |
|-----------------|--------------------------------------------------|
| **EC2**         | Amazon Elastic Compute Cloud - Compute           |
| **RDS**         | Amazon Relational Database Service               |
| **Redshift**    | Amazon Redshift                                  |
| **ElastiCache** | Amazon ElastiCache                               |
| **Elasticsearch** | Amazon Elasticsearch Service                   |

These service aliases should be used under the services section in your configuration YAML file when setting up Reserved Instances (RI) utilization budget alerts.


## Configuration File Example

In the `config` folder, you will find a sample YAML file named `aws_budget_config_sample.yml`. This file is pre-configured with an example AWS Budget setup. You can use this file as a template and modify the values according to your requirements .

### Example for Whole Account Budget

```yaml
---
budget_alerting:
  - whole_account_budget:
      aws_profile: 'AWS_PROFILE_NAME'
      account_id: 'AWS_ACCOUNT_ID'
      budget_name: 'Whole-Account-Budget'
      budget_type: 'COST'
      budget_time_unit: 'MONTHLY'
      budget_limit_amount: '2000'
      budget_limit_unit: 'USD'
      cost_types_parameters:
        IncludeTax: true
        IncludeSubscription: true
        UseBlended: false
        IncludeRefund: false
        IncludeCredit: false
        IncludeUpfront: true
        IncludeRecurring: true
        IncludeOtherSubscription: true
        IncludeSupport: true
        IncludeDiscount: true
        UseAmortized: false
      actual_budget_comparison_operator: 'GREATER_THAN'
      actual_budget_threshold: 90.0
      forecasted_budget_comparison_operator: 'GREATER_THAN'
      forecasted_budget_threshold: 80.0
      threshold_type: 'PERCENTAGE'
      actual_threshold_notification: 'ACTUAL'
      forecasted_threshold_notification: 'FORECASTED'
      recreate_budget_if_needed: true
      email_addresses:
        - "your.email@example.com"
actions_on:
  - budget_alerting


``` 

### Example for Service Basis Alerting

```yaml
---
- account_service_budget:
      aws_profile: 'AWS_PROFILE_NAME'
      account_id: 'AWS_ACCOUNT_ID'
      budget_name: 'Overall-Service-Budget'
      budget_type: 'COST'
      budget_time_unit: 'MONTHLY'
      budget_limit_amount: '1000'
      budget_limit_unit: 'USD'
      cost_types_parameters:
        IncludeTax: true
        IncludeSubscription: true
        UseBlended: false
        IncludeRefund: false
        IncludeCredit: false
        IncludeUpfront: true
        IncludeRecurring: true
        IncludeOtherSubscription: true
        IncludeSupport: true
        IncludeDiscount: true
        UseAmortized: false
      actual_budget_comparison_operator: 'GREATER_THAN'
      actual_budget_threshold: 90.0
      forecasted_budget_comparison_operator: 'GREATER_THAN'
      forecasted_budget_threshold: 80.0
      threshold_type: 'PERCENTAGE'
      actual_threshold_notification: 'ACTUAL'
      forecasted_threshold_notification: 'FORECASTED'
      recreate_budget_if_needed: true
      email_addresses:
        - "your.email@example.com"
      cost_filters:
        services:
          - "AWS Services Alias"

actions_on:
  - budget_alerting

```

### Example for Reserved Instance Alerting 

```yaml
---
- ri_utilization_budget:
      aws_profile: 'AWS_PROFILE_NAME'
      account_id: 'AWS_ACCOUNT_ID'
      budget_name: 'RI-Utilization-Budget'
      budget_type: 'RI_UTILIZATION'
      budget_time_unit: 'MONTHLY'
      actual_budget_comparison_operator: 'LESS_THAN'
      actual_budget_threshold: 80.0
      threshold_type: 'PERCENTAGE'
      actual_threshold_notification: 'ACTUAL'
      recreate_budget_if_needed: true
      email_addresses:
       - "rajat.vats@opstree.com"
       - "piyush.upadhyay@opstree.com"
      cost_filters:
        services:
          - "SNS"

actions_on:
  - budget_alerting

```

# Usage

## Running Locally with Python
Ensure you have Python and the required dependencies installed:

```bash
pip install -r requirements.txt
```
Export the path to your configuration file:
```bash
export CONF_PATH="/path/to/your/config/aws_budget_config_sample.yml"
```
Move to **scripts** directory
```bash
cd /scripts
```
Run the Python script:
```bash
python3 aws_budget_factory.py
```
## Running with Docker
Ensure you have installed Docker & Make in your machine

 Build the Docker image:
```yml
make build
```
Run the Docker container:
```yml
make run
```


## Pricing

- [`AWS Cost Management Pricing`](https://aws.amazon.com/aws-cost-management/aws-budgets/pricing/) - For details on AWS Budgets pricing, please visit the page.

## Resources docs


- [`AWS Cost Management and Cost Control using AWS Budgets`](https://medium.com/@vanchi811/aws-cost-management-and-cost-control-using-aws-budgets-467df3b72227) - A detailed guide on AWS cost management practices.


## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 2.0 |
| <a name="requirement_python"></a> [python](#requirement\_python) | >= 3.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 2.0 |


## Authors

This project was developed and is maintained by the following individuals:

- [Piyush Upadhyay](https://github.com/piiiyuushh)
