# Sample Cloud Platform Repository

This repository contains infrastructure-as-code (IaC) and configuration-as-code (CasC) source code for the Sample Azure Cloud Platform stacks and individual resources, currently on Azure, provisioned by Terraform and automated by Ansible.

## !!Important!!
Terraform state file is stored in Azure Blob storage account,
TODO: Use Azure AD authentication instead of storage access key.
Target subscription/Environment is automatically determined by the branch the code is running from.

## Source Code

This repository houses code inside `infra` folder.

## Toolchain

The following tools are required to develop and debug the code locally:
- Azure CLI 2.37.0 +
- Python 3.8+
- Ansible 2.8+ or Ansible core 2.13+
- Terraform 1.4.4 +
- Kubectl Client 1.21.0 + (For AKS resources only)

## Deployments

Execution of IaC code are through pipelines on different criteria and branch policies. During development and debugging, intended changes can be previewed. The key principle is automation enables end-to-end orchestration (provisioning/configuration) with as close as possible to zero touch.

**Formal change management procedure must be followed for any production deployments or updates.**

# Maintainers

This repository is maintained by the Sample DevOps Team.
