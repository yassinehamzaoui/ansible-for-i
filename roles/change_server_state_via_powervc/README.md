change_server_state_via_powervc
=========
Ansible role for starting, stopping a VM via PowerVC.

Role Variables
--------------

| Variable                                            | Type          | Description                                                               |
|-----------------------------------------------------|---------------|---------------------------------------------------------------------------|
| `change_server_state_via_powervc_vm_action`         | str           | Specifies Perform the given action. Valid choices are stop, start         |
| `change_server_state_via_powervc_vm_name`           | str           | Specifies the vm name or id.                                              |
| `change_server_state_via_powervc_project`           | str           | Optional. Default value is "ibm-default".                                 |
| `change_server_state_via_powervc_project_domain`    | str           | Optional. Default value is "Default".                                     |
| `change_server_state_via_powervc_user_domain_name`  | str           | Optional. Default value is "Default".                                     |
| `change_server_state_via_powervc_validate_certs`    | bool          | Optional. Default value is True.                                          |
| `change_server_state_via_powervc_timeout`           | int           | Optional. Default value is 1800 (seconds).                                |

Return Variables
--------------

| Variable                                           | Type          | Description                                                       |
|----------------------------------------------------|---------------|-------------------------------------------------------------------|
| `change_server_state_via_powervc_server_result`    | dict          | Result of VM state change                     |

Example Playbooks
----------------
```
- name: Stop a vm
  hosts: powervc 
  tasks:
    - include_role:
        name: change_server_state_via_powervc
      vars:
        change_server_state_via_powervc_vm_action: 'stop'
        change_server_state_via_powervc_vm_name: 'vm1'
        change_server_state_via_powervc_validate_certs: false

```

```
- name: Start a vm 
  hosts: powervc

  roles:
    - role: change_server_state_via_powervc
      vars:
        change_server_state_via_powervc_vm_action: 'start'
        change_server_state_via_powervc_vm_name: 'vm1'
        change_server_state_via_powervc_validate_certs: false
```

License
-------

Apache-2.0
