# Unlocking On-Premise Infrastructure Automation: Terraform with VMware vSphere

In today’s fast-paced IT landscape, automation is no longer a luxury—it’s a necessity. While cloud infrastructure often steals the spotlight, many organizations still rely heavily on on-premise environments, particularly VMware vSphere, for their critical workloads. The good news? Terraform, the industry-leading Infrastructure as Code (IaC) tool, isn’t just for the cloud. It can also automate and manage your on-premise VMware infrastructure seamlessly.

In this article, I’ll walk you through how to use Terraform to deploy a virtual machine (VM) on VMware vSphere. By the end, you’ll have a working example and a deeper understanding of how Terraform can bridge the gap between cloud and on-premise infrastructure.

---

## Why Terraform for VMware vSphere?

Terraform’s declarative approach allows you to define your infrastructure as code, making it reproducible, version-controlled, and easy to manage. With the [vSphere provider](https://registry.terraform.io/providers/hashicorp/vsphere/latest), you can automate tasks such as:

- Deploying virtual machines
- Configuring networks and storage
- Managing resources like clusters, datastores, and folders

This eliminates manual processes, reduces human error, and ensures consistency across your on-premise environment.

---

## Tutorial: Deploying a VM on VMware vSphere Using Terraform

Let’s dive into a practical example. We’ll use Terraform to deploy a virtual machine on VMware vSphere. Below are the steps to get started.

### Prerequisites

1. **Terraform Installed**: Download and install Terraform from [here](https://www.terraform.io/downloads.html).
2. **VMware vSphere Access**: Ensure you have access to a vSphere environment with the necessary permissions.
3. **vSphere Provider**: Terraform’s vSphere provider will be used to interact with your vSphere environment.

---

### Step 1: Set Up Your Terraform Configuration

Create a new directory for your Terraform configuration and navigate into it:

```bash
mkdir terraform-vsphere-vm
cd terraform-vsphere-vm
```

Create a file named `main.tf` and add the following configuration:

```hcl
# main.tf
provider "vsphere" {
  user           = "your-vsphere-username"
  password       = "your-vsphere-password"
  server         = "your-vsphere-server"
  allow_unverified_ssl = true
}

data "vsphere_datacenter" "dc" {
  name = "Datacenter"
}

data "vsphere_datastore" "datastore" {
  name          = "datastore1"
  datacenter_id = data.vsphere_datacenter.dc.id
}

data "vsphere_compute_cluster" "cluster" {
  name          = "Cluster"
  datacenter_id = data.vsphere_datacenter.dc.id
}

data "vsphere_network" "network" {
  name          = "VM Network"
  datacenter_id = data.vsphere_datacenter.dc.id
}

data "vsphere_virtual_machine" "template" {
  name          = "ubuntu-template"
  datacenter_id = data.vsphere_datacenter.dc.id
}

resource "vsphere_virtual_machine" "vm" {
  name             = "terraform-vm"
  resource_pool_id = data.vsphere_compute_cluster.cluster.resource_pool_id
  datastore_id     = data.vsphere_datastore.datastore.id

  num_cpus = 2
  memory   = 4096
  guest_id = data.vsphere_virtual_machine.template.guest_id

  network_interface {
    network_id   = data.vsphere_network.network.id
    adapter_type = data.vsphere_virtual_machine.template.network_interface_types[0]
  }

  disk {
    label            = "disk0"
    size             = data.vsphere_virtual_machine.template.disks.0.size
    eagerly_scrub    = data.vsphere_virtual_machine.template.disks.0.eagerly_scrub
    thin_provisioned = data.vsphere_virtual_machine.template.disks.0.thin_provisioned
  }

  clone {
    template_uuid = data.vsphere_virtual_machine.template.id

    customize {
      linux_options {
        host_name = "terraform-vm"
        domain    = "example.com"
      }

      network_interface {}
    }
  }
}
```

---

### Step 2: Replace Placeholder Values

Update the following placeholders in the `main.tf` file with your vSphere environment details:

- `your-vsphere-username`: Your vSphere username.
- `your-vsphere-password`: Your vSphere password.
- `your-vsphere-server`: The address of your vSphere server.
- `Datacenter`: The name of your vSphere datacenter.
- `datastore1`: The name of your datastore.
- `Cluster`: The name of your compute cluster.
- `VM Network`: The name of your network.
- `ubuntu-template`: The name of your VM template.

---

### Step 3: Initialize and Apply the Configuration

1. Initialize Terraform to download the vSphere provider:

   ```bash
   terraform init
   ```

2. Review the execution plan:

   ```bash
   terraform plan
   ```

3. Apply the configuration to deploy the VM:

   ```bash
   terraform apply
   ```

   Confirm the action by typing `yes` when prompted.

---

### Step 4: Verify the Deployment

Once Terraform completes the deployment, log in to your vSphere client and verify that the VM named `terraform-vm` has been created successfully.

---

### Step 5: Clean Up

To destroy the VM and clean up resources, run:

```bash
terraform destroy
```

---

## Example Repository

To make it easier for you to get started, I’ve added this example to my GitHub repository. You can find it under the `onpremise/vmware/vm-deployment` directory:

[GitHub Repository: Terraform Examples for Cloud and On-Premise (VMware)](https://github.com/your-username/terraform-examples)

---

## Why This Matters

By leveraging Terraform for VMware vSphere, you can:

- **Standardize VM deployments**: Ensure consistency across your infrastructure.
- **Reduce manual effort**: Automate repetitive tasks and focus on higher-value work.
- **Integrate with CI/CD pipelines**: Combine Terraform with tools like Jenkins or GitLab for seamless automation.

Whether you’re managing a hybrid environment or fully on-premise, Terraform empowers you to treat your infrastructure as code, bringing the same agility and efficiency to your VMware environment as you would expect in the cloud.

---

## Final Thoughts

Terraform’s versatility makes it a game-changer for infrastructure automation, regardless of where your workloads reside. If you’re already using Terraform for the cloud, extending it to your on-premise VMware environment is a natural next step.

Give the example a try, and let me know your thoughts in the comments! If you have any questions or need further assistance, feel free to reach out.

#Terraform #VMware #InfrastructureAsCode #DevOps #OnPremise #Automation #vSphere

--- 

Happy automating! 🚀