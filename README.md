# [ad_auth](#ad_auth)

Bind a system to Active Directory.

|Travis|GitHub|Quality|Downloads|
|------|------|-------|---------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-ad_auth.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-ad_auth)|[![github](https://github.com/robertdebock/ansible-role-ad_auth/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-ad_auth/actions)|[![quality](https://img.shields.io/ansible/quality/47535)](https://galaxy.ansible.com/robertdebock/ad_auth)|[![downloads](https://img.shields.io/ansible/role/d/47535)](https://galaxy.ansible.com/robertdebock/ad_auth)|

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
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
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

For verification `molecule/resources/verify.yml` run after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: yes

  tasks:
    - name: check adcli
      command: /usr/sbin/adcli --help
    - name: check realmd
      command: /usr/sbin/realm list
    - name: check samba common tools
      command: /usr/bin/net --version
    - name: check pam_krb5.so
      stat:
        path: /usr/lib64/security/pam_krb5.so
      register: ad_auth_pam_krb5_so
    - name: assert pam_krb5.so
      assert:
        that:
          - ad_auth_pam_krb5_so.stat.exists | bool
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
```

## [Requirements](#requirements)

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.epel
- robertdebock.python_pip

```

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/ad_auth.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|el|7|
|fedora|31|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.



## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-ad_auth) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-ad_auth/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
