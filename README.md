# Ansible Role nutanix-guest-tools

Installe ngt on linux vm.

## Playbook example
```yml
- name: Enable and install NGT
  hosts: myserver
  # vars_prompt:
  #   - name: "nutanix_prism_user"
  #     prompt: "Enter Nutanix username (ex: user@domain.local)"
  #     private: no
  #   - name: "nutanix_prism_password"
  #     prompt: "Enter password"
  #     private: yes
  vars_files:
    - /etc/ansible/secret/nutanix_credentials_vars.yml
  roles:
    - nutanix-guest-tools
```