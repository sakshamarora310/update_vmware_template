# Ansible Role: VMware Content Library Template Auto-Updater

This Ansible role automates the full lifecycle of updating VMware Content Library templates for RHEL9
It is designed for Platform/Cloud/VMware engineers who want hands-off image management with reliability, repeatability, and minimal manual intervention.
This ansible playbook is to update Linux (RHEL/ CentOS/ Oracle Linux) Templates

## 🚀 Features

* Clones a VM from existing content library template
* Renames the template to -old via vcenter API
* Updates the rhel template via DNF
* Converts a VM into a template automatically
* Uploads/updates the template inside a vCenter Content Library
* Includes fault-tolerant block/rescue logic

## 📦 Requirements

* Ansible 2.15+ (recommended) (Tested on version 2.17.12)
* `vmware.vmware_rest`, `community.vmware`,`vmware.vmware`collection
* vCenter 7.0+
* Credentials with privileges to manage templates and library items
* govc (https://github.com/vmware/govmomi/tree/main/govc)

Install required collections:

```bash
ansible-galaxy collection install vmware.vmware_rest
```

## 📁 Role Structure

```
roles/
update_vmware_template/
├── tasks
│   ├── main.yml
│   ├── post_update.yml
│   ├── pre_update.yml
│   ├── rollback.yml
│   └── update_tasks.yml
└── vars
    ├── main.yml
    └── sensitive.yml (ansible-vault)
```

## 📘 Example Playbook

```yaml
---

- name: "Update Template Playbook"
  hosts: all
  gather_facts: false
  ignore_unreachable: true
  vars_files:
    - "main.yml"
    - "sensitive.yml"
  connection: local
  roles:
    - update_vmware_template

```

## 🧪 Testing

* Tested on RHEL 9
* Validated on vCenter 7.0 & 8.0

© 2025 Saksham Arora
