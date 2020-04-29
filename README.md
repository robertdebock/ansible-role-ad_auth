# ad_auth

Install and configure ad_auth on your system.

|Travis|GitHub|Quality|Downloads|
|------|------|-------|---------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-ad_auth.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-ad_auth)|[![github](https://github.com/robertdebock/ansible-role-ad_auth/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-ad_auth/actions)|[![quality](https://img.shields.io/ansible/quality/47535)](https://galaxy.ansible.com/robertdebock/ad_auth)|[![downloads](https://img.shields.io/ansible/role/d/47535)](https://galaxy.ansible.com/robertdebock/ad_auth)|

## Example Playbook

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.ad_auth
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
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
    - name: check authconfig
      command: /usr/sbin/authconfig --help
    - name: check krb5 workstation
      command: /usr/bin/kdestroy
    - name: check realmd
      command: /usr/sbin/realm list
    - name: check samba common tools
      command: /usr/bin/net --version
    - name: check samba winbindd
      command: /usr/sbin/winbindd
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## Role Variables

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for ad_auth

# The realm to connect to, for example "XYZ/example.com"
ad_auth_realm: ""

# The hash to register to AD, for example: "a1b2c3"
ad_auth_registration_hash: ""

# The user to register to AD, for example: "bind_user"
ad_auth_registration_user: ""

# The OU to search in, for example: "ou=Nerds,ou=Staff"
ad_auth_ou: ""

# The server to bind to, for example: "ad.example.com"
ad_auth_server: xxx

```

## Requirements

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap

```

## Context

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/ad_auth.png "Dependency")

## Compatibility

This role has been tested on these [container images](https://hub.docker.com/):

|container|tags|
|---------|----|
|el|7|

The minimum version of Ansible required is 2.7 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.



## Testing

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

## License

Apache-2.0


## Author Information

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
