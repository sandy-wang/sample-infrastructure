# Azure stacks provisioner

## Folder structure
The folder layout is simple and straight forwards, can be restructured when role and custom modules are introduced.
<https://docs.ansible.com/ansible/2.8/user_guide/playbooks_best_practices.html#directory-layout>

- `files`        - Plaintext files that contains configuration for certain resources
- `group_vars`   - Ansible variables, all.yml - list variables that have same value among all subscriptions, dev.yml - variables that only apply to dev subscription
- `handles`      - Trigger certain operation when a change is made on a target host.
- `inventory`    - Inventory defines the hosts or groups you want Ansible to run against.
- `tf_templates` - Ansible Jinja2 template on Terraform. Top level contains files that are common between all Azure stack, az_xxx contains templates for specific stack, az_xxx is the stack_name.
- `playbook.yml` - One playbook that can provision and manage all Azure stacks in one subscription or single stack in one subscription when stack_name is provided.
- `pipelines`    - Azure pipelines that call ansible playbook from different branches


This is an Ansible playbook for provisioning and configuring Azure resources.

## TL;DR

Preview the configuration change for all resources in dev subscription

    ansible-playbook -vv playbook.yml \
        --extra-vars app_env=dev \
        --tags preview

Preview the configuration change for rg_network stack in dev subscription

    ansible-playbook -vv playbook.yml \
        --extra-vars app_env=dev \
        --extra-vars stack_name=rg_network \
        --tags preview

Update an already provisioned stack in the dev subscription (only pipeline does this)

    ansible-playbook -vv playbook.yml \
        --extra-vars app_env=dev \
        --tags deploy

Destroy an existing stack (must use force delete flag)

    ansible-playbook -vv playbook.yml \
        --extra-vars app_env=dev \
        --extra-vars force_delete=true \
        --tags destroy

## Configuration

### Application Environment

The following application environments are supported, allowing for the configuration of resources at both supported Azure regions:

#### Australia East Region
- dev
- stage
- prod


#### Australia Southeast Region
- dev-dr
- prod-dr

## Pre-reqs

Need to have the following before proceeding:

- For local development, run "az login" to login as yourself to the DEV environment
- Pipeline agents with the tools installed
  - Ansible
  - Terraform
  - Azure CLI

## Components

### Azure

#### Azure Resource Group

Azure Resource Groups for each subscription.

## References

### Terraform
<https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs>
