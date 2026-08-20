# Deploying KAI-IB Controller and Agent in AWS

## Introduction

This solution uses a CloudFormation Template to deploy a KAI-IB Controller and a KAI-IB Client Agent in an Amazon Virtual Private Cloud.

This is a new VPC template, meaning all necessary resources will be created from scratch, including VPC, subnets, route tables, Internet Gateway, NAT Gateway, security groups, and VPC Flow Logs.

See the Template Parameters section for more details. The Client Agent has two interfaces. The first interface (eth0) is used for control plane communication with the Controller. The second interface (eth1) is used for test traffic. The agent automatically registers with the Controller on launch.

## Template Parameters

The following table lists the parameters for this deployment.

| **Parameter label (name)** | **Default** | **Description** |
| --- | --- | --- |
| Stack name | Requires input | Specify the deployment stack name. The stack name can contain a maximum of 9 alphanumeric characters. If you are deploying multiple times in the same environment, make sure to use a unique name. |
| Username | Requires input | Email ID of the stack owner. All resources created by this stack are tagged with Username. |
| Project | `KAIIB-AWS` | The name of the project where this stack will be used. |
| Availability Zone | Requires input | Availability Zone to use for the subnets in the VPC. Select from the drop-down list. |
| VPC | `172.16.0.0/16` | The CIDR block for the VPC. |
| KAIIB Controller AMI ID | Requires input | The AMI ID of the KAI-IB Controller image for the selected region. |
| Management Subnet for KAIIB Controller | `172.16.1.0/24` | This subnet is attached to the KAI-IB Controller and is used to access the Controller UI. |
| KAIIB Agent AMI ID | Requires input | The AMI ID of the KAI-IB Agent image for the selected region. |
| Deploy Client Agent | `yes` | Whether to deploy the Client Agent. Select `yes` or `no`. |
| Display Agents by tags in KAIIB UI | `yes` | Creates an IAM role to allow agents to read EC2 tags for display in the Controller UI. Select `yes` or `no`. |
| Instance Type for KAIIB Agents | `c5.2xlarge` | The EC2 instance type to use for the KAI-IB Agent instance. It is recommended to use at least `c5.2xlarge`. |
| SSH Key | Requires input | Name of an existing EC2 KeyPair to enable SSH access to the KAI-IB instances. |
| Control Subnet for KAIIB Agents | `172.16.2.0/24` | KAI-IB agents will use this subnet for control plane communication with the Controller. |
| Test Subnet for KAIIB Agents | `172.16.3.0/24` | KAI-IB agents will use this subnet for test traffic. |
| Authentication Username | `admin` | Username for agent to controller authentication. |
| Authentication Password | `admin` | Password for agent to controller authentication. |
| Authentication Fingerprint | | Fingerprint for agent to controller authentication - OPTIONAL. |
| Allowed Subnet for Security Group | `1.1.1.1/1` | Subnet range allowed to access deployed AWS resources. Execute `curl ifconfig.co` to know your IP or google for "what is my IP". Default value is a dummy value. User must provide a proper subnet range. |

## Post Deployment

After successful deployment of the stack, follow the instructions below:

- Go to the EC2 Dashboard and look for the deployed instances.
- Select the Controller instance and note the public IP.
- Open your browser and access the KAI-IB Controller UI with URL `https://<Controller Public IP>` (Default Username/Password: `admin`/`admin`).
- The registered KAI-IB agent should appear in the Controller UI automatically.
- A KAI-IB license needs to be procured for further usage. The license needs to be configured at **Administration** > **License Manager** in the Controller UI.
