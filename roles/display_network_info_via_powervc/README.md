display_network_info_via_powervc
=========
Ansible role for retrieving port info and corresponding subnet info by mac address.

Role Variables
--------------

| Variable                                             | Type          | Description                                                            |
|------------------------------------------------------|---------------|------------------------------------------------------------------------|
| `display_network_info_via_powervc_mac_addr`          | dict          | Required. The mac address of a port to be retrieved.                   |
| `display_network_info_via_powervc_project`           | str           | Optional. Default value is "ibm-default".                              |
| `display_network_info_via_powervc_project_domain`    | str           | Optional. Default value is "Default".                                  |
| `display_network_info_via_powervc_user_domain_name`  | str           | Optional. Default value is "Default".                                  |
| `display_network_info_via_powervc_validate_certs`    | bool          | Optional. Default value is True.                                       |

Return Variables
--------------

| Variable                                           | Type          | Description                                                       |
|----------------------------------------------------|---------------|-------------------------------------------------------------------|
| `display_network_info_via_powervc_interface_info`  | dict          | Dictionary with network interface information                     |

Example Playbooks
----------------
```
- name: Retrieve port info and subnet info by mac address
  hosts: powervc 
  tasks:
    - include_role:
        name: display_network_info_via_powervc
      vars:
        display_network_info_via_powervc_mac_addr: "fa:16:3e:cd:45:ee"
        display_network_info_via_powervc_validate_certs: false

```

Example Output
----------------
        "display_network_info_via_powervc_interface_info": {
            "fixed_ips": [
                {
                    "ip_address": "11.11.11.21",
                    "subnet_id": "8b5ec1f0-a104-4a9c-b374-c08bffff3dca"
                }
            ],
            "mac_addr": "fa:16:3e:cd:45:ee",
            "subnet": [
                {
                    "allocation_pools": [
                        {
                            "end": "11.11.11.111",
                            "start": "11.11.11.2"
                        }
                    ],
                    "cidr": "11.11.11.0/24",
                    "created_at": "2020-11-02T01:51:21Z",
                    "description": "",
                    "dns_nameservers": [
                        "9.0.128.50"
                    ],
                    "enable_dhcp": false,
                    "gateway_ip": "11.11.11.1",
                    "host_routes": [],
                    "id": "8b5ec1f0-a104-4a9c-b374-c08bffff3dca",
                    "ip_version": 4,
                    "ipv6_address_mode": null,
                    "ipv6_ra_mode": null,
                    "name": "",
                    "network_id": "6d42b2e2-ebb7-4744-87a7-53520440267d",
                    "project_id": "1b7a20fcc60c4b6e88fe725463af9438",
                    "revision_number": 0,
                    "service_types": [],
                    "subnetpool_id": null,
                    "tags": [],
                    "tenant_id": "1b7a20fcc60c4b6e88fe725463af9438",
                    "updated_at": "2020-11-02T01:51:21Z"
                }
            ]
        }

License
-------

Apache-2.0
