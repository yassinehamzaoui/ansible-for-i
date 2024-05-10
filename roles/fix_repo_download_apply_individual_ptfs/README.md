fix_repo_download_apply_individual_ptfs
=========

Check if requested individual PTFs are already in catalog. If not, will download non-existent PTFs and write information into catalog.
After that, will transfer savfs to the target server, then load and apply PTFs.

Role Variables
--------------

| Variable                                                  | Type          | Description                                                            |
|-----------------------------------------------------------|---------------|------------------------------------------------------------------------|
| `fix_repo_download_apply_individual_ptfs_ptfs_list_parm`  | list          | The list of PTFs that need to be applied.     |
| `fix_repo_download_apply_individual_ptfs_repo_server`     | str           | Specifies the SNDPTFORD server used to download ptfs.     |
| `fix_repo_download_apply_individual_ptfs_temp_or_perm`    | str           | Used by apply_ptf role. Controls whether the target PTFs will be permanent applied or temporary applied. Value can be  '*TEMP' or '*PERM'. Default value is '*TEMP'.                     |

Return Variables
--------------

| Variable                                                                   | Type          | Description                                                       |
|----------------------------------------------------------------------------|---------------|-------------------------------------------------------------------|
| `fix_repo_download_apply_individual_ptfs_final_ptfs_status_with_requisite` | dict          | The dict of all the PTFs' status including requisite PTFs. |
| `fix_repo_download_apply_individual_ptfs_original_ptfs_status`             | dict          | The dict of the original requested PTFs' status.     |
| `fix_repo_download_apply_individual_ptfs_requisite_ptfs_status`            | dict          | The dict of the requisite PTFs' status.   |

Example Playbook
----------------
```
- name: IBM i download a list of individual PTFs
  hosts: testhost

  vars:
    fix_repo_download_apply_individual_ptfs_ptfs_list_parm: ["SI73751", "SI74612", "SI74136"]
    fix_repo_download_apply_individual_ptfs_repo_server: systemA

  tasks:
    - name: Include fix_repo_download_apply_individual_ptfs role to download a list of individual ptfs
      include_role:
        name: fix_repo_download_apply_individual_ptfs
```

Example Returned Variables
----------------
```
"fix_repo_download_apply_individual_ptfs_final_ptfs_status_with_requisite": {
        "SI70936": "APPLIED",
        "SI74136": "APPLIED",
        "SI74612": "APPLIED",
        "SI73751": "APPLIED"
    }
"fix_repo_download_apply_individual_ptfs_original_ptfs_status": {
        "SI74136": "APPLIED",
        "SI74612": "APPLIED"
    }
"fix_repo_download_apply_individual_ptfs_requisite_ptfs_status": {
        "SI70936": "APPLIED"
    }
```

License
-------

Apache-2.0
