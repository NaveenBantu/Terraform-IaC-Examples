# Terraform Example: Deploy a Simple EC2 Instance on AWS

This example demonstrates how to use Terraform to deploy a simple EC2 instance on AWS.

---

## Prerequisites

1. **Terraform Installed**: Download and install Terraform from [here](https://www.terraform.io/downloads.html).
2. **AWS CLI Configured**: Ensure you have configured your AWS CLI with the necessary credentials. Run `aws configure` to set up your credentials.

---

## Usage

1. Clone this repository:

   ```bash
   git clone https://github.com/your-username/terraform-aws-ec2.git
   cd terraform-aws-ec2
   ```

2. Initialize Terraform:

   ```bash
   terraform init
   ```

3. Review the execution plan:

   ```bash
   terraform plan
   ```

4. Apply the configuration to deploy the EC2 instance:

   ```bash
   terraform apply
   ```

   Confirm the action by typing `yes` when prompted.

5. Verify the deployment:

   - The EC2 instance ID and public IP address will be displayed in the output.
   - Log in to the AWS Management Console to verify the instance.

6. Clean up:

   To destroy the EC2 instance and clean up resources, run:

   ```bash
   terraform destroy
   ```

---

## Inputs

| Name           | Description                          | Type   | Default                     |
|----------------|--------------------------------------|--------|-----------------------------|
| `aws_region`   | The AWS region to deploy the instance | string | `"us-east-1"`               |
| `ami_id`       | The AMI ID for the EC2 instance      | string | `"ami-0c55b159cbfafe1f0"`   |
| `instance_type`| The instance type for the EC2 instance | string | `"t2.micro"`                |

---

## Outputs

| Name          | Description                          |
|---------------|--------------------------------------|
| `instance_id` | The ID of the EC2 instance           |
| `public_ip`   | The public IP address of the EC2 instance |

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```

---

## How It Works

1. **Provider Configuration**: The `provider "aws"` block specifies the AWS region where the resources will be deployed.
2. **EC2 Instance Resource**: The `aws_instance` resource defines the EC2 instance, including the AMI ID, instance type, and tags.
3. **Input Variables**: Variables like `aws_region`, `ami_id`, and `instance_type` allow you to customize the deployment.
4. **Outputs**: The `outputs.tf` file displays the instance ID and public IP address after deployment.

---

## Example Output

After running `terraform apply`, you’ll see output similar to this:

```
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

instance_id = "i-0123456789abcdef0"
public_ip = "54.123.45.67"
```

---

## Clean Up

To avoid unnecessary charges, destroy the resources after testing:

```bash
terraform destroy
```

---

This example provides a simple yet powerful way to automate EC2 instance deployments using Terraform. Feel free to customize it further to suit your needs! 🚀