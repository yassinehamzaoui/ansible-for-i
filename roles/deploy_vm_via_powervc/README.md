deploy_vm_via_powervc
=========
The ansible role for creating a VM via PowerVC.

Role Variables
--------------

| Variable                                            | Type         | Description                                      |
|-----------------------------------------------------|--------------|--------------------------------------------------|
| `deploy_vm_via_powervc_image_name_or_id`            | str          | Required. The name or id of the base image to boot.                   |
| `deploy_vm_via_powervc_vm_name`                     | str          | Required. Specifies the name of the deployed vm.                      |
| `deploy_vm_via_powervc_flavor_name_or_id`           | str          | The name or id of the flavor in which the new instance has to be created. |
| `deploy_vm_via_powervc_nic_list`                    | str          | Required. A list of networks to which the instance's interface should be attached. |
| `deploy_vm_via_powervc_deploy_timeout`              | str          | The amount of time the module should wait for the instance to get into active state..                   |
| `deploy_vm_via_powervc_deploy_userdata`             | str          | Opaque blob of data which is made available to the instance.  |
| `deploy_vm_via_powervc_availability_zone_name`      | str          | The availability zone in which to create the server. |
| `deploy_vm_via_powervc_key_name_shown_on_powervc`   | str          | The key pair name to be used when creating an instance. |
| `deploy_vm_via_powervc_project`                     | str          | Optional. Default value is "ibm-default".                              |
| `deploy_vm_via_powervc_project_domain`              | str          | Optional. Default value is "Default".                                  |
| `deploy_vm_via_powervc_user_domain_name`            | str          | Optional. Default value is "Default".                                  |
| `deploy_vm_via_powervc_validate_certs`              | bool         | Optional. Default value is True.                                       |

Return Variables
--------------

| Variable                                           | Type          | Description                                                       |
|----------------------------------------------------|---------------|-------------------------------------------------------------------|
| `deploy_vm_via_powervc_server_info`                | dict          | Deployed VM information                     |


Example Playbooks
----------------
```
- name: Deploy a vm
  hosts: powervc 
  tasks:
    - include_role:
        name: deploy_vm_via_powervc
      vars:
        deploy_vm_via_powervc_vm_name: 'Abc' 
        deploy_vm_via_powervc_image_name_or_id: 'image1'
        deploy_vm_via_powervc_nic_list: [{
                "fixed_ip": "9.5.163.102",
                "net-name": "net-163"
            }]
        deploy_vm_via_powervc_validate_certs: false

```

License
-------

Apache-2.0
