apply_ptf
=========

Apply all loaded ptfs or apply a set of ptfs according to the given ptfs list, and return ptfs applied status. Then perform an IPL if auto_ipl is set to true and at least one PTF requests an IPL for permanent applied or temporary applied

Role Variables
--------------

| Variable                          | Type          | Description                                                            |
|-----------------------------------|---------------|------------------------------------------------------------------------|
| `apply_ptf_to_be_applied_list`   | list           | ptfs list will be applied. ptf_id and product are required.|
| `apply_ptf_apply_all_loaded_ptfs`| bool          | Controls whether all loaded ptf will be applied. When its value is true, 'apply_ptf_to_be_applied_list' will be ignored. The default value is true.    |
| `apply_ptf_temp_or_perm`         | str          | Controls whether the target PTFs will be permanent applied or temporary applied. Value can be  '*TEMP' or '*PERM'. Default value is '*TEMP'.                     |
| `apply_ptf_delayed_option`       | str          | Controls whether the PTF is delayed apply or not. Value can be '*YES', '*NO' or '*IMMDLY'. Default value is '*IMMDLY'.                      |
| `apply_ptf_auto_ipl`             | bool           | Controls whether an immediate reboot will be launched automatically if at least one ptf requests an IPL for permanent applied or temporary applied. The default value is false. |


Return Variables
--------------

| Variable                                     | Type          | Description                                                       |
|----------------------------------------------|---------------|-------------------------------------------------------------------|
| `apply_ptf_apply_fail_with_requisite_list`      | list          | The list of failed apply when apply_ptf_to_be_applied_list is provided.                                        |
| `apply_ptf_apply_fail_dict`      | dict          | The list of failed apply when apply_ptf_to_be_applied_list is provided.                                        |
| `apply_ptf_requisite_list`      | list          | The list of failed apply when apply_ptf_to_be_applied_list is provided.                                        |
| `apply_ptf_apply_success_list`   | list          | The list of successful apply when apply_ptf_to_be_applied_list is provided and apply_ptf_apply_all_loaded_ptfs set to True.   |
| `apply_ptf_apply_fail_list`      | list          | The list of failed apply when apply_ptf_to_be_applied_list is provided and apply_ptf_apply_all_loaded_ptfs set to True.   |

Example Playbook
----------------
```
- name: IBM i apply a set of single PTFs one by one
  hosts: testhost

  vars:
    apply_ptf_to_be_applied_list:
      - {'ptf_id':'SI73543', 'product':'5770UME'}
      - {'ptf_id':'SI73430', 'product':'5733SC1'}

  tasks:
    - name: apply a list of single ptfs
      include_role:
        name: apply_ptf
```

```
- name: IBM i apply a set of single PTFs immediately, all those PTFs are applied permanently.
  hosts: testhost

  vars:
    apply_ptf_to_be_applied_list:
      - {'ptf_id':'SI73543', 'product':'5770UME'}
      - {'ptf_id':'SI73430', 'product':'5733SC1'}
    apply_ptf_temp_or_perm: '*PERM'
    apply_ptf_delayed_option: '*NO'
    apply_ptf_auto_ipl: false

  tasks:
    - name: apply a list of single ptfs
      include_role:
        name: apply_ptf
```

```
- name: IBM i apply all loaded ptfs and IPL the system if at least one PTF requires an IPL for permanent applied or temporary applied.
  hosts: ibmi

  roles:
    - role: apply_ptf
      vars:
        apply_ptf_apply_all_loaded_ptfs: true
        apply_ptf_temp_or_perm: '*PERM'
        apply_ptf_delayed_option: '*NO'
        apply_ptf_auto_ipl: true
```

Example Returned Variables
----------------
```
"apply_ptf_apply_fail_with_requisite_list": [
        {
            "ptf_id": "SI74612",
            "requisite": "SI74559"
        },
        {
            "ptf_id": "SI74136",
            "requisite": "SI70936"
        }
    ]
"apply_ptf_apply_fail_dict": {
        "SI74136": "APPLY_FAIL",
        "SI74612": "APPLY_FAIL"
    }
"apply_ptf_requisite_list": [
        "SI74559",
        "SI70936"
    ]
```

License
-------

Apache-2.0
