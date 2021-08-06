# ansible-manage-user ⚙️ #

[![GitHub Build Status](https://github.com/cisagov/ansible-manage-user/workflows/build/badge.svg)](https://github.com/cisagov/ansible-manage-user/actions)
[![Total alerts](https://img.shields.io/lgtm/alerts/g/cisagov/ansible-manage-user.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/cisagov/ansible-manage-user/alerts/)
[![Language grade: Python](https://img.shields.io/lgtm/grade/python/g/cisagov/ansible-manage-user.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/cisagov/ansible-manage-user/context:python)

Ansible playbooks to manage a user account on a set of hosts.

These are the actions that are currently supported:

- Create a new user account and add a public ssh key to its
  `authorized_keys` file, with the option to allow the user to run
  privileged commands via `sudo`
- Delete an existing user account and all of its directories and files

## Warning ⚠️ ##

These commands can be damaging, so always double-check the id of the user
that you plan to manage!

## Pre-requisites ##

- You must run these playbooks as a user that has ssh access to and
  sudo privileges on each target host in your inventory.
- You must create an Ansible inventory file at the root of this
  project containing the name or IP address of each target host on
  which you wish to manage users.  A sample inventory file might look
  like this:

  ```yaml
  all:
    hosts:
      my_ungrouped_host:
    children:
      group1:
        hosts:
          my_server:
          my_database:
      group2:
        hosts:
          sample.mydomain.com:
          db.mydomain.com:
      group2:
        hosts:
          192.168.1.5:
          192.168.1.6:
  ```

- Ansible supports more complicated inventory management.  If you have
  a need for that, consult the [Ansible
  documentation](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)
  for more information.
- You must create a directory `group_vars` at the root of this project
  that contains files with the Ansible variable values for each group
  specified in the inventory; for example, to specify the same values
  for every host in the inventory you might create a single file named
  `all.yml` that looks like this:

  ```yaml
  allow_sudo: true
  ansible_become: yes
  username: audit
  ssh_public_key: "{{ lookup('aws_ssm', /ssh/public/key) }}"
  ```

## Usage ##

### Adding a new user account ###

```console
ansible-playbook --inventory=inventory.yml create/playbook.yml
```

### Deleting an existing user account ###

```console
ansible-playbook --inventory=inventory.yml delete/playbook.yml
```

## Contributing ##

We welcome contributions!  Please see [`CONTRIBUTING.md`](CONTRIBUTING.md) for
details.

## License ##

This project is in the worldwide [public domain](LICENSE).

This project is in the public domain within the United States, and
copyright and related rights in the work worldwide are waived through
the [CC0 1.0 Universal public domain
dedication](https://creativecommons.org/publicdomain/zero/1.0/).

All contributions to this project will be released under the CC0
dedication. By submitting a pull request, you are agreeing to comply
with this waiver of copyright interest.

## Author Information ##

David Redmin - <david.redmin@trio.dhs.gov>
