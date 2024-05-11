display_vm_info_via_powervc
=========
An Ansible role for displaying a VM via PowerVC.

Role Variables
--------------

| Variable                                        | Type          | Description                                      |
|-------------------------------------------------|---------------|--------------------------------------------------|
| `display_vm_info_via_powervc_vm_name`           | str           | Required. Specifies the name of deployed vm.     |
| `display_vm_info_via_powervc_project`           | str           | Optional. Default value is "ibm-default".        |
| `display_vm_info_via_powervc_project_domain`    | str           | Optional. Default value is "Default".            |
| `display_vm_info_via_powervc_user_domain_name`  | str           | Optional. Default value is "Default".            |
| `display_vm_info_via_powervc_validate_certs`    | bool          | Optional. Default value is True.                 |

Return Variables
--------------

| Variable                                           | Type          | Description                                                       |
|----------------------------------------------------|---------------|-------------------------------------------------------------------|
| `display_vm_info_via_powervc_vm_info_result`       | dict          | Dictionary with vm information                                    |

Example Playbooks
----------------
```
- name: Retrieve vm information a vm
  hosts: powervc 
  tasks:
    - include_role:
        name: display_vm_info_via_powervc
      vars:
        display_vm_info_via_powervc_vm_name: 'Abc'
        display_vm_info_via_powervc_validate_certs: false

```

License
-------

Apache-2.0
