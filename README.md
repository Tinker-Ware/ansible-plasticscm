Plastic SCM Server Ansible Role
===============================

This is a role to **install** and **configure**  a [Plastic SCM](https://www.plasticscm.com/) Server
-- A source control management for big projects --

**Default variables are located in default/main.yml.**
By default, it installs a ready to use Server.
(Token and licence are provided by the user as a variable and file respectively)

Dependencies
------------

None.

Use this out of the box
=======================

To install all the defaults:

```
- hosts: my_server
  roles:
      - { role: plasticscm, become: yes }
```

Defining Variables
==================

You can provide a variable sector for your host like this:

Example of `host_vars/my_serever`

```
distro_id: "Debian_8.1"

users:
  - name: example_user
    password: pass
    groups:
      - example_group

language: "en"
working_mode: "UPWorkingMode"
security_config: "::389:::"
buffer_pool_size: 0
audit_log_level: 1
audit_log_file: "audit.log"
create_default_rep: true
limit_to_load_pusher_guid_table_in_full: 0
database_upgrade_disabled: false
is_enterprise_setup: false
fips_compliant: false

provider_name: "sqlite"

plastic_token: "mytoken"

```

The very basic Variables:
-------------------------
( Check out `defaults/main.yml` for advanced variables )

### Target Distribution

`distro_id`: Specifies the target distribution.

  - Default:
    * `Debian_8.1`
  - Possible values are: (The ones supported by plastic)
    * `Debian_6.0`
    * `Debian_8.1`
    * `Ubuntu_14.04`
### Server Configuration

Variables that will be placed inside your `plasticscm/server/server.conf`

#### Language

`language`: The language of your server.

  - Default:
    * `en`
  - Possible values are:
    * `en`
    * `es`

#### Working mode

`working_mode`: Defines the authentication method between server and client.

  - Default:
    * `UPWorkingMode`
  - Possible values are:
    * `NameWorkingMode`
    * `NameIDWorkingMode`
    * `LDAPWorkingMode`
    * `ADWorkingMode`
    * `UPWorkingMode`
    * `TubeWorkingMode`

#### Database
`provider_name`: Defines the databse provider
  - Default:
    * `sqlite`

### Users and groups

An array containing users and the groups they belong to.

```
users:
  - name: example_user
    password: pass
    groups:
      - example_group1
      - example_group2
```

### Token

`plastic_token: "mytoken"`: The token provided by PlasticSCM

### Licence File

The Licence file for your server must be placed in:
`{{ inventory_dir }}/host_files/{{ inventory_hostname }}/plasticd.lic`
Structure follows the [Ansible Best Practices Directory Layout](http://docs.ansible.com/ansible/playbooks_best_practices.html#directory-layout)

For example, include your Licence file in the top level of the directory
(the pathname of the directory holding Ansible’s inventory host file) in
a path named:
`/host_files/my_server/plasticd.lic`
Doing this will include your licence in your server.

This way there is no need to inlcude the file inside the rol, providing
it as a parameter instead.


Author Information
==================

This role is provided by the [Tinkerware](http://tinkerware.io) project
under a **GNU GPLv3** Licence.
