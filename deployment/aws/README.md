# About KAI-IB AWS CloudFormation Templates

## Introduction

Welcome to the repository for Keysight KAI-IB CloudFormation templates for deploying KAI-IB with Amazon Web Services.

To start using KAI-IB CFT templates, please see the **README** files in each individual directory and decide on which template to start with from the below list.

## Prerequisites

The prerequisites are:
- KAI-IB Controller and Agent AMI IDs for your target AWS region. Contact your Keysight representative if AMIs are not available in your region.
- Key pair for management access to KAI-IB instances.
- Permissions to create AWS Identity and Access Management (IAM) roles; these roles are required for Keysight KAI-IB Agent to interact with the AWS environment.
- Permissions to create subnets.
- Permissions to create and access interfaces.
- User must be associated with managed IAM policy **"AWSCloudFormationFullAccess"** and a custom IAM policy.

Note:
    JSON format for custom policy

    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "VisualEditor0",
                "Effect": "Allow",
                "Action": [
                    "iam:*",
                    "cloudformation:*",
                    "ec2:*",
                    "logs:*",
                    "elasticip:*"
                ],
                "Resource": "*"
            }
        ]
    }

## Specialized Knowledge

Before you deploy a CloudFormation template, we recommend that you become familiar with the following AWS services:
- [Amazon EC2](https://docs.aws.amazon.com/ec2/index.html)
- [Amazon Elastic Block Store (Amazon EBS)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html)
- [Amazon VPC](https://docs.aws.amazon.com/vpc/index.html)
- [AWS CloudFormation](https://docs.aws.amazon.com/cloudformation/index.html)

If you are new to AWS, see [Getting Started with AWS](https://aws.amazon.com/getting-started/).

## Supported Instance Types

The supported instance types are:
- For the KAI-IB Controller, the supported instance type is c5.2xlarge.
- For KAI-IB Agents, the supported instance types are c5.2xlarge and c5n.9xlarge.

## List of Supported KAI-IB CloudFormation Templates for AWS Deployments

The following is a list of the current supported KAI-IB CloudFormation templates. Click the links to view the README files which include deployment details.

### I. [Controller and Single Agent](controller_and_single_agent):

This template deploys:
- One KAI-IB Controller, in a public subnet.
- One KAI-IB Client Agent having two interfaces. One interface is for control plane communication with the Controller, and the other interface is for test traffic.
- A new VPC with all necessary networking resources (subnets, route tables, Internet Gateway, NAT Gateway, security groups, and VPC Flow Logs).

### Template Information

Descriptions for each template are contained at the top of each template in the Description key. For additional information and assistance in deploying a template, see the README file in the individual template directory.

### AWS Rights

AmazonEC2FullAccess needs to be given to the user that will create the deployments using CloudFormation templates.

## Troubleshooting and Limitations

### Troubleshooting

- I encountered a **CREATE_FAILED** error when I tried deploying the CloudFormation template:

If AWS CloudFormation fails to create the stack, it is recommended that you relaunch the template with **Rollback on failure** set to **No**. You can find this setting in **Options** > **Advanced** in the AWS CloudFormation console.
With this setting, the stack's state is retained, and the instance is left running so you can troubleshoot the issue.

When you set the **Rollback on failure** setting to **No**, you will continue to incur AWS charges for this stack. Make sure to delete the stack when you finish troubleshooting. For additional information, see [Troubleshooting AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/troubleshooting.html) on the AWS website.

- I encountered a size limitation error when I deployed the AWS CloudFormation template:

If you deploy the templates from a local copy on your computer or from a non-S3 location, you might encounter template size limitations when you create the stack.
For more information about AWS CloudFormation limits, see the [AWS](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html) documentation.
