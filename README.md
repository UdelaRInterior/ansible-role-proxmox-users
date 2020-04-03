Proxmox Users
=========

The ansible role `proxmox-users` aims to manage te proxomox users and groups association to pam accounts, as well as Proxomx permissions.

This role takes example from and uses [ansible-users](https://github.com/UdelaRInterior/ansible-users) role.

Requirements
------------



Role Variables
--------------

`pve_users` is a structure compatible with `users` variable of ansible-users role. 

`pve_groups` is a structure compatible with `os_groups`  variable of ansible-users role.

`pve_permissions` is a list of the following dict structure: 
```yaml
- path: <proxmox_datacenter_path>
- user: <user> (and no "group:" defined)
- group: <group> (and no "user:" defined)
- role: <proxmox role>
```
Either the key `user:` or the the key `group` must be defined, not both. 

Dependencies
------------

This role doen't perform the unix users and groups creation, which are needed. This can be done before in the playbook with the role [ansible-users](https://github.com/UdelaRInterior/ansible-users).


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

GPL-v3

Author Information
------------------

(c) 2020 UdelaR Interior, Daniel Viñar, @ulvida