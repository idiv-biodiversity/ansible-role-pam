Pluggable Authentication Modules
================================

Deploys PAM configuration.


Table of Contents
-----------------

<!-- toc -->

- [Requirements](#requirements)
- [Role Variables](#role-variables)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Top-Level Playbook](#top-level-playbook)
  * [Role Dependency](#role-dependency)
- [License](#license)
- [Author Information](#author-information)

<!-- tocstop -->


Requirements
------------

- Ansible 2.9


Role Variables
--------------

```yml
# unlock default keyring when user logs in
pam_gnome_keyring: no

# use nslcd to provide passwd, group and shadow
pam_ldap: no

# create home directory from skeleton if it doesn't exist
pam_mkhomedir: no
```


Dependencies
------------

```yml
---

# requirements.yml

roles:

  # only needed for pam_ldap
  - name: idiv_biodiversity.nslcd
    src: https://github.com/idiv-biodiversity/ansible-role-nslcd
    version: vX.Y.Z

  # only neede for pam_ldap
  - name: idiv_biodiversity.nsswitch
    src: https://github.com/idiv-biodiversity/ansible-role-nsswitch
    version: vX.Y.Z

  - name: idiv_biodiversity.pam
    src: https://github.com/idiv-biodiversity/ansible-role-pam
    version: vX.Y.Z

...
```


Example Playbook
----------------

### Top-Level Playbook

Write a top-level playbook:

```yml
---

- name: server
  hosts: server

  roles:
    - role: idiv_biodiversity.pam
      tags:
        - pam

...
```

### Role Dependency

Define the role dependency in `meta/main.yml`:

```yml
---

dependencies:

  - role: idiv_biodiversity.pam
    tags:
      - pam

...
```


License
-------

MIT


Author Information
------------------

This role was created in 2023 by [Christian Krause][author] aka [wookietreiber
at GitHub][wookietreiber], HPC cluster systems administrator at the [German
Centre for Integrative Biodiversity Research (iDiv)][idiv].


[author]: https://www.idiv.de/en/groups_and_people/employees/details/61.html
[idiv]: https://www.idiv.de/
[wookietreiber]: https://github.com/wookietreiber
