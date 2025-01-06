# Terraform Examples for Cloud and On-Premise (VMware) Infrastructure as Code (IaC)

This repository contains a collection of Terraform examples demonstrating how to use Terraform for Infrastructure as Code (IaC) across various cloud providers and on-premise environments (specifically VMware). These examples are designed to help you get started with Terraform and provide reusable templates for common infrastructure scenarios.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Repository Structure](#repository-structure)
- [Cloud Examples](#cloud-examples)
- [On-Premise (VMware) Examples](#on-premise-vmware-examples)
- [Getting Started](#getting-started)
- [Contributing](#contributing)
- [License](#license)

## Introduction

Terraform is a powerful tool for managing infrastructure as code, allowing you to define, provision, and manage resources across multiple Cloud Providers and On-Premise(VMware) environments. Whether you're managing cloud resources or virtualized infrastructure on-premise, these examples will help you get started with Terraform.

## Prerequisites

Before using the examples in this repository, ensure you have the following installed:

- **Terraform**: [Download and install Terraform](https://www.terraform.io/downloads.html)
- **Terraform Providers**:
  - Cloud providers (e.g., AWS, Azure, GCP)
  - VMware vSphere provider
- **Required Tools**:
  - Git
  - CLI tools for your cloud provider (e.g., AWS CLI, Azure CLI)
  - VMware vSphere access (for on-premise examples)

## Repository Structure

```
terraform-examples/
├── cloud/
│   ├── aws/
│   │   ├── ec2-instance/
│   │   ├── s3-bucket/
│   │   └── vpc/
│   ├── azure/
│   │   ├── vm/
│   │   ├── storage-account/
│   │   └── vnet/
├── onpremise/
│   └── vmware/
│       ├── vm-deployment/
│       ├── network-config/
│       └── datastore-management/
├── README.md
└── LICENSE
```

## Cloud Examples

The `cloud/` directory contains examples for deploying infrastructure on popular cloud platforms such as AWS, Azure, and GCP. Each subdirectory includes a Terraform configuration for a specific use case.

### AWS
- **EC2 Instance**: Deploy a simple EC2 instance.
- **S3 Bucket**: Create an S3 bucket with basic configuration.
- **VPC**: Set up a Virtual Private Cloud (VPC) with subnets and security groups.

### Azure
- **Virtual Machine**: Deploy a virtual machine in Azure.
- **Storage Account**: Create a storage account with a container.
- **Virtual Network**: Set up a virtual network with subnets.

## On-Premise (VMware) Examples

The `onpremise/` directory focuses on VMware vSphere, providing examples for managing on-premise infrastructure using Terraform.

### VMware vSphere
- **VM Deployment**: Deploy a virtual machine in a vSphere environment.
- **Network Configuration**: Configure virtual networks and port groups.
- **Datastore Management**: Manage datastores and storage resources.

## Getting Started

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/terraform-examples.git
   cd terraform-examples
   ```

2. Navigate to the desired example directory:
   ```bash
   cd cloud/aws/ec2-instance
   ```

3. Initialize Terraform:
   ```bash
   terraform init
   ```

4. Review the Terraform plan:
   ```bash
   terraform plan
   ```

5. Apply the configuration:
   ```bash
   terraform apply
   ```

6. Destroy the infrastructure (when no longer needed):
   ```bash
   terraform destroy
   ```

## Contributing

Contributions are welcome! If you have additional examples or improvements, please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or fix.
3. Commit your changes.
4. Submit a pull request.

Please ensure your contributions align with the repository's structure and include appropriate documentation.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

Feel free to explore the examples and adapt them to your specific use cases. If you have any questions or suggestions, please open an issue or reach out to the maintainers. Happy Terraforming! 🚀
