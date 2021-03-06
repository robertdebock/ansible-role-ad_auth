# [ad_auth](#ad_auth)

DEPRECATION WARNING: This repository is not maintained anymore; This role only runs on CentOS 7 and required pip modules, but since [end of 2020](https://www.python.org/doc/sunset-python-2/) there is no development on python 2 anymore.

Bind a system to Active Directory.

|GitHub|GitLab|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![github](https://github.com/robertdebock/ansible-role-ad_auth/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-ad_auth/actions)|[![gitlab](https://gitlab.com/robertdebock/ansible-role-ad_auth/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-ad_auth)|[![quality](https://img.shields.io/ansible/quality/47535)](https://galaxy.ansible.com/robertdebock/ad_auth)|[![downloads](https://img.shields.io/ansible/role/d/47535)](https://galaxy.ansible.com/robertdebock/ad_auth)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-ad_auth.svg)](https://github.com/robertdebock/ansible-role-ad_auth/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.ad_auth
      ad_auth_registration_username: my_username
      ad_auth_registration_password: my_password
      ad_auth_ou: ou=Nerds,ou=Staff
      ad_auth_server: my_server.example.com
      ad_auth_domain: my_domain.local
      ad_auth_join: no
      ad_auth_simple_allow_users:
        - my_user_1
        - my_user_2
```

The machine needs to be prepared in CI this is done using `molecule/resources/prepare.yml`:
```yaml
---
- name: prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.epel
    - role: robertdebock.python_pip
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for ad_auth

# The username to register to AD, for example: "bind_user"
ad_auth_registration_username: "unset"

# The password to register to AD, for example: "MyPaSsWoRd"
ad_auth_registration_password: "unset"

# The OU to search in, for example: "ou=Nerds,ou=Staff"
ad_auth_ou: "unset"

# The server to bind to, for example: "ad.example.com"
ad_auth_server: "unset"

# The domain to use for SSSD configuration, for example: "example.com"
ad_auth_domain: "usnet.local"

# Should this role try to bind to the AD server?
# (This can be unset for automated testing)
ad_auth_join: yes

# To limit selected users to login, fill this list with users that are
# allowed to login:
# ad_auth_simple_allow_users:
#   - my_user_1
#   - my_user_2
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-ad_auth/blob/master/requirements.txt).

## [Status of requirements](#status-of-requirements)

The following roles are used to prepare a system. You may choose to prepare your system in another way, I have tested these roles as well.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
| [robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-bootstrap)
| [robertdebock.epel](https://galaxy.ansible.com/robertdebock/epel) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-epel/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-epel/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-epel/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-epel)
| [robertdebock.python_pip](https://galaxy.ansible.com/robertdebock/python_pip) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-python_pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-python_pip/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-python_pip/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-python_pip)

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/ansible-role-ad_auth/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|el|7|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.



If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-ad_auth/issues)

## [License](#license)

Apache-2.0

## [Contributors](#contributors)

I'd like to thank everybody that made contributions to this repository. It motivates me, improves the code and is just fun to collaborate.

- [aindenko](https://github.com/aindenko)

## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
