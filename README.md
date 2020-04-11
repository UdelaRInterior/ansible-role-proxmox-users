Proxmox Users
=========

The Ansible role `proxmox-users` aims to manage te Proxomox users (linked to pam accounts) as well as groups and Proxomox permissions.

This role takes example from [`udelarinterior.users`](https://github.com/UdelaRInterior/ansible-users) role, an can be used with it to create PAM accounts and associated Proxmox users.

Requirements
------------

This role has to be ran against a Proxmox server (phisical or virtual) or one or several nodes of Proxmox cluster. 


Role Variables
--------------

* `pve_users` is the structure of users' data:
```
pve_users:
- username: user1
  name: User One
  email: user1@domain.org
  firstname: User
  lastname: One 
- username: user2
  name: User Two
  expire: 8600   # in seconds
- username: user3
  name: User Three
```
`pve_users` variable is some how compatible with [`users` variable](https://github.com/UdelaRInterior/ansible-users/blob/master/README.md#variables) of [`udelarinterior.users`](https://github.com/UdelaRInterior/ansible-users) role. While they don't have the same set of attributes, bosth `udelarinterior.users` and `udelarinterior.proxmos_users` can be stored in the same variable at the playbook level.

* `pve_groups` is the structure of the groups' data:
```
pve_groups:
- name: group1
  comment: Group One
  members:
  - user1
  - user2
- name: group2
  comment: Group Two
  members:
  - user2
  - user3
```
On the same way, this variable is compatible with [`os_groups` variable](https://github.com/UdelaRInterior/ansible-users/blob/master/README.md#variables) of [`udelarinterior.users`](https://github.com/UdelaRInterior/ansible-users) role.

* `pve_permissions` is the structure of persmissions data. It is a list of the following dict: 
```yaml
- path: <proxmox_datacenter_path>
  user: <user> (and no "group:" defined)
  group: <group> (and no "user:" defined)
  role: <proxmox role>
```
Either the key `user:` or the the key `group:` must be defined, not both. 

Dependencies
------------

This role doen't perform the unix users and groups creation, which are needed. This can be done before in the playbook with the role [ansible-users](https://github.com/UdelaRInterior/ansible-users).


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: proxmox_nodes
      vars:
        my_users:
          <definition of your proxmox users>
        my_groups:
          <definition of your proxmox groups>
        my_permissions:
          <definition of your proxmox permissions>
      roles:
         - role: username.rolename
          vars:
            pve_users: "{{ my_users }}"
            pve_groups: "{{ my_groups }}"
            pve_permissions: "{{ my_permissions }}"

License
-------

GPL-v3

Author Information
------------------

(c) 2020 UdelaR Interior, Daniel Viñar, @ulvida