# ansible-manage-user ⚙️ #

[![Build Status](https://travis-ci.com/cisagov/ansible-manage-user.svg?branch=develop)](https://travis-ci.com/cisagov/ansible-manage-user)

Ansible playbooks to manage a user account on a set of hosts.

These are the actions that are currently supported:

* Create a new user account and add a public ssh key to its
  `authorized_keys` file, with the option to allow the user to run
  privileged commands via `sudo`
* Delete an existing user account and all of its directories and files

## Warning ⚠️ ##

These commands can be damaging, so always double-check the id of the user
that you plan to manage!

## Pre-requisites ##

* You must run these playbooks as a user that has ssh access to each target host
  in your inventory and sudo privileges on each target host.
* You must create a simple inventory file containing the name or IP address
  of each target host that you wish to manage users on (one host per line).
  A sample inventory file might look like this:

  ```console
  my_server
  my_database
  sample.mydomain.com
  db.mydomain.com
  192.168.1.5
  192.168.1.6
  ```

  Ansible supports more complicated inventory management.  If you have a need for
  that, consult the [Ansible
  documentation](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)
  for more information.
* When adding a new user, the user's public ssh key must be stored as a
  parameter in
  [AWS SSM](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html).

## Usage ##

### Adding a new user account ###

```console
ansible-playbook --inventory=inventory.txt create/playbook.yml --extra-vars="username=USERID ssm_public_key=/PATH/TO/KEY" --become
```

### Adding a new privileged user account (allowed to sudo) ###

```console
ansible-playbook --inventory=inventory.txt create/playbook.yml --extra-vars="allow_sudo=true username=USERID ssm_public_key=/PATH/TO/KEY" --become
```

### Deleting an existing user account ###

```console
ansible-playbook --inventory=inventory.txt delete/playbook.yml --extra-vars="username=USERID" --become
```

## Contributing ##

We welcome contributions!  Please see [here](CONTRIBUTING.md) for
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
