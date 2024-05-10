load_apply_ptfs
=========

Call load_ptf role and apply_ptfs role to load and apply a list of individual ptfs, and return status.

Role Variables
--------------

| Variable                                  | Type          | Description                                                                    |
|-------------------------------------------|---------------|--------------------------------------------------------------------------------|
| `load_apply_ptfs_to_be_loaded_ptf_list`   | list       | The not loaded ptfs' information list. ptf_id, product and file_name are required.|
| `load_apply_ptfs_loaded_list`             | list     | Already loaded but not applied ptfs' list. ptf_id and product are required.        |
| `load_apply_ptfs_remote_lib`          | str           | The remote lib stores ptfs' savf.  The default value is QGPL.                             |
| `load_apply_ptfs_apply_all_loaded_ptf`| bool          | Used by apply_ptf role. Controls whether all loaded ptf will be applied. When the value is true, 'to_be_applied_list' will be ignored. The default value is True.    |
| `load_apply_ptfs_temp_or_perm`        | str           | Used by apply_ptf role. Controls whether the target PTFs will be permanent applied or temporary applied. Value can be  '*TEMP' or '*PERM'. Default value is '*TEMP'.                     |
| `load_apply_ptfs_delayed_option`      | str           | Used by apply_ptf role. Controls whether the PTF is delayed apply or not. Value can be '*YES', '*NO' or '*IMMDLY'. Default value is '*IMMDLY'.                     |
| `load_apply_ptfs_auto_ipl`            | bool          | Used by apply_ptf role. Controls whether an immediate reboot will be launched automatically if at least one ptf requests an IPL for permanent applied or temporary applied. The default value is false. |

Return Variables
--------------

| Variable                                          | Type          | Description                   |
|---------------------------------------------------|---------------|-------------------------------|
| `load_apply_ptfs_load_success_list`   | list          | The list of the successful load.  |
| `load_apply_ptfs_load_fail_list`      | list          | The list of the failed load.      |
| `load_apply_ptfs_load_fail_dict`      | dict          | The dict of the failed load. The key is the ptf id, and the value is the ptf status.|
| `load_apply_ptfs_apply_fail_with_requisite_list`      | list          | The list of failed apply when to_be_applied_list is provided.                                        |
| `load_apply_ptfs_apply_fail_dict`      | dict          | The list of failed apply when to_be_applied_list is provided.                                        |
| `load_apply_ptfs_requisite_list`      | list          | The list of failed apply when to_be_applied_list is provided.                                        |
| `load_apply_ptfs_apply_success_list`   | list          | The list of successful apply when to_be_applied_list is provided and load_apply_ptfs_apply_all_loaded_ptf set to True.   |
| `load_apply_ptfs_apply_fail_list`      | list          | The list of failed apply when to_be_applied_list is provided and load_apply_ptfs_apply_all_loaded_ptf set to True.   |

Example Playbook
----------------
```
- name: Load a list of individual ptfs on an ibm i system, then apply
  hosts: desthost

  vars:
    load_apply_ptfs_to_be_loaded_ptf_list:
      - {'ptf_id':'SI73543', 'product':'5770UME', 'file_name':'QSI73543.file'}
      - {'ptf_id':'SI73430', 'product':'5733SC1', 'file_name':'QSI73430.file'}
    load_apply_ptfs_loaded_list:
      - {'ptf_id':'SI63556', 'product':'5770UME'}
      - {'ptf_id':'SI71714', 'product':'5733SC1'}
    load_apply_ptfs_temp_or_perm: '*PERM'
    load_apply_ptfs_delayed_option: '*IMMDLY'
    load_apply_ptfs_auto_ipl: False

  tasks:
    - name: Include load_apply_ptfs role to Load and apply a list of single ptfs.
      include_role:
        name: load_apply_ptfs
      register: load_apply_result
```
Example Returned Variables
----------------
```
"load_apply_ptfs_load_success_list": [
        {
            "file_name": "QSI73751.FILE",
            "product": "5733SC1",
            "ptf_id": "SI73751",
        }
]
"load_apply_ptfs_load_fail_list": [
        {
            "file_name": "QSI73962.FILE",
            "product": "5770JV1",
            "ptf_id": "SI73962",
        }
]
"load_apply_ptfs_load_fail_dict": {
        "SI73962": "OPTION_NOT_INSTALLED_OR_ALREADY_INSTALLED"
    }
"load_apply_ptfs_apply_fail_with_requisite_list": [
        {
            "ptf_id": "SI74612",
            "requisite": "SI74559"
        },
        {
            "ptf_id": "SI74136",
            "requisite": "SI70936"
        }
    ]
"load_apply_ptfs_apply_fail_dict": {
        "SI74136": "APPLY_FAIL",
        "SI74612": "APPLY_FAIL"
    }
"load_apply_ptfs_requisite_list": [
        "SI74559",
        "SI70936"
    ]
```
License
-------

Apache-2.0
