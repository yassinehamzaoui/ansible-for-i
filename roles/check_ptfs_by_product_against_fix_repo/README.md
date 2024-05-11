check_ptfs_by_product_against_fix_repo
=========

Compare the PTF status with specific product id on IBM i against fix repository, and returned the PTFs' status list

Role Variables
--------------

| Variable                                              | Type          | Description                                               |
|-------------------------------------------------------|---------------|-----------------------------------------------------------|
| `check_ptfs_by_product_against_fix_repo_product`      | string        | the product of PTFs will be checked.                      |
| `check_ptfs_by_product_against_fix_repo_repo_server`  | string        | repository server name registered in inventory.           |

Return Variables
--------------

| Variable                                              | Type          | Description                                               |
|-------------------------------------------------------|---------------|-----------------------------------------------------------|
| `check_ptfs_by_product_against_fix_repo_ptf_status`   | list          | The list of PTF status.                                   |

Example Playbook
----------------
```
- name: check the ptfs by product on IBM i against fix repository
  hosts: ibmi

  vars:
    check_ptfs_by_product_against_fix_repo_product: "5770SS1"
    check_ptfs_by_product_against_fix_repo_repo_server: "repo_server_name"

  tasks:
    - name: check product ptf
      include_role:
        name: check_ptfs_by_product

    - name: print ptfs status
      debug:
        var: check_ptfs_by_product_against_fix_ptf_status

```

Return Value Example
----------------
```
"check_ptfs_by_product_against_fix_repo_ptf_status": [
    {
        "PRODUCT": "5770SS1",
        "PRODUCT_STATUS": "OK",
        "PTF_LIST": [
            {
                "PTF_IDENTIFIER": "SI69340",
                "PTF_STATUS": "NON-EXISTENT"
            },
            {
                "PTF_IDENTIFIER": "SI69764",
                "PTF_STATUS": "NON-EXISTENT"
            },
            {
                "PTF_IDENTIFIER": "SI70544",
                "PTF_LOADED_STATUS": "APPLIED"
            }
        ]
    }
]
```

License
-------

Apache-2.0
