# Ansible VM Provisioner Role

This Ansible role automates the provisioning of virtual machines using Vagrant with Terraform as the provisioner and VirtualBox as the provider.

## Role Variables

### General Setup
| Variable                      | Default Value       | Description                          |
|-------------------------------|---------------------|--------------------------------------|
| terraform_install_path        | /usr/local/bin      | Installation path for Terraform      |
| ansible_python_interpreter    | /usr/bin/python3    | Python interpreter path              |
| terraform_version             | "1.8.5"             | Default Terraform version            |

### Terraform Provider
| Variable                                  | Default Value       | Description                          |
|-------------------------------------------|---------------------|--------------------------------------|
| vm_provisioner_terraform_provider_source  | "bmatcuk/vagrant"   | Terraform provider source            |
| vm_provisioner_terraform_provider_version | "~> 4.1.0"          | Provider version constraint          |

### VM Configuration
| Variable                          | Default Value       | Description                          |
|-----------------------------------|---------------------|--------------------------------------|
| vm_provisioner_name               | "alma9"             | Default VM name                      |
| vm_provisioner_box_name           | "generic/alma9"     | Vagrant box name                     |
| vm_provisioner_box_version        | "4.3.12"            | Vagrant box version                  |
| vm_provisioner_vagrant_files_base_dir | "alma9-generic" | Vagrantfiles directory               |

Example host configuration:
```yaml
vm_provisioner_hosts:
  - hostname: "vm-1"
    ip: "{{ available_ip }}"
    memory_mb: 4096
    cpus: 2
    forwarded_ports:
      - { guest: 2222, host: 2222 }
      - { guest: 8080, host: 8080 }
```

Example playbook:
```yaml
- hosts: localhost
  connection: local
  roles:
    - check-available-ips
    - vm_provisioner
```

* clone check-available-ips role [here](https://github.com/kasimerbay/vm-provisioner.git)

### Requirements
- Ansible 2.9+
- Debian-based systems
- Python 3
- Internet access

### License
- MIT