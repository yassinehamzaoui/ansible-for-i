# Change Log

## v3.0.0 (2024-05-10)

This release includes the final changes to ensure continued compliance with the Redhat certification process.
This is a disruptive API change with the collection roles that impacts the naming of all the role variables and
role return variables. All user playbooks using roles must be updated in order to work with this release.
Each role README file fully documents the new role variable names and the naming convention used is noted below.

The following changes are included with this release:

- Ansible lint clean up for fix management use cases.
- Clean-up of role variables to use a global naming convention that prepends the role name to each role variable
  and role return variable.   For example, with the apply_ptf role, the variable "to_be_applied_list"
  is now "apply_ptf_to_be_applied_list". This convention is followed 99% of the time. This change with roles required
  updating all the use cases and also the role integration tests.
- Numerous fixes for the role integration tests along with updating PTFs used in the tests. This is still a work in progress.
- Various fixes for issues that became apparent with the global role variable naming.

## v2.0.2 (2024-04-24)

This release primarily addresses the fix check breakage from the recent PSP web site updates.

### Bug Fixes

- Fix for github issue 191: <https://github.com/IBM/ansible-for-i/issues/191>
  - Revise parsing of PSP group PTF web page for recent change that broke the fix check modules.
  - Future work is needed to properly account for individual PTF dependencies with new web page format
    along with other lower level information.

- Fix for github issue 194: <https://github.com/IBM/ansible-for-i/issues/194>
  - Increase timeout for fix check modules from 10 to 60 seconds to account for increased PSP web page access time
    that was causing false failures in roles that depend on fix check.

- Fix the level 1 fix management module ibmi_fix_repo_lv1
  - Revise parsing of sha256 file that is used for checksums when generating a new database fix entry for a refresh action.
    The file format has changed slightly and we were erroneously skipping valid fixes that were using the new format.

## v2.0.1 (2024-03-05)

This release includes a number of fixes along with code clean-up to continue the Redhat certification of the collection.

The plan for the next release is to complete the Redhat certification clean-up by modifying the role variables to follow the convention
of the role name prepended to the role variable, e.g., the role sync_apply_ptf_group with role variable src_host will rename the role variable to sync_apply_ptf_group_src_host. This future change with role variables will obviously impact user playbooks that utilize the collection roles.

### Bug Fixes

- Fix for github issue 163: <https://github.com/IBM/ansible-for-i/issues/163>
  - Binary dependency should reference python3 instead of python.
  - Add collection dependencies in requirements file.

- Fixes for github issue #177 for sync_apply_ptf_group: <https://github.com/IBM/ansible-for-i/issues/177>
  - Correct role documentation examples for sync_apply_ptf_group and sync_apply_ptf_group_networkinstall for the ptf information.
  - Fix a bug in sync_apply_ptf_group with incorrect server variable for delegation

- Fix for role sync_apply_individual_ptfs_lv1.
  - Found a common bug for role sync_apply_individual_ptfs_lv1 as previously found for the role sync_apply_ptf_group in github issue 177.

- Fix for github issue 146. Resolve deprecated warnings: <https://github.com/IBM/ansible-for-i/issues/146>
  - Remove use of deprecated call _remote_checksum and instead use _execute_remote_stat, which impacts a few modules.

### Code clean-up

- Ansible lint clean up for most of the uses cases
  - Cleaning up cicd-cli, ibmi_services, and security_management use cases.
  - Clean up use cases for cicd-tower, towerapi, and db2mirror_setup_via_powervc.

### Documentation

- Fix documentation for various modules (github issue 179): <https://github.com/IBM/ansible-for-i/issues/179>
  - Correct botched collection name in various module examples that are used in the module documentation.

- Documentation clean up for ibmi_tcp_server_service: <https://github.com/IBM/ansible-for-i/issues/164>
  - Clarify the example for restarting ssh server with ibmi_tcp_server_service to address github issue 164.

## v2.0.0 (2023-11-22)

With this release the collection now requires ansible-core version 2.14 or 2.15 on the Ansible server / control node. This also requires having Python 3.9 on the Ansible server / control node. The IBM i target nodes may still run at a lower level of Python 3. These changes are necessary for continued Redhat certification of the collection and also for Ansible Galaxy.

### Bug Fixes

- Fixes for ansible 2.14 and 2.15 (primarily sanity test related).
- Fix present_ip_interface role which was broken due to some incorrect var names defined in defaults/main.yml.

### Miscellaneous

- Modifications for ansible-lint in production mode that are a work in progress for the collection (rest of changes in following release).
  - Completely clean up playbooks.
  - Extensive clean up of roles (but additional work required to change role variables / API for all roles).

### Documentation

- Document new requirements for ansible-core version 2.14+ and python version 3.9. Add new Ansible install instructions for an IBM i Ansible server.
- Add CHANGELOG file

## v1.9.2 (2023-11-21)

This is a patch release with code and documentation fixes.

### Bug Fixes

- Fix for github issue #153:  HTTP Error 403-Forbidden, being returned from IBM service web servers with the fix check modules http/https requests (<https://github.com/IBM/ansible-for-i/issues/153>).
- Fix for github issue #157: fix_group_check dead URL (<https://github.com/IBM/ansible-for-i/issues/157>).
- Fix in check_pfs role for incorrect reference to temporarily_applied_list.

### Miscellaneous

- Update checking for playbooks/ibmi-sysval-sample.yml.
- Update load_ptf return option in log_load_fail_info.yml (OPTION_NOT_INSTALLED_OR_ALREADY_INSTALLED).

### Documentation

- Document required configuration of *SRVLAN for network install (usecases/fix_management/sync_apply_ptf_group_networkinstall.yml, roles/sync_apply_ptf_group_networkinstall/README.md).
