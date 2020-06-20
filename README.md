# Ansible Role: sshuttle

Ansible role for installing [`sshuttle`](https://sshuttle.readthedocs.io/en/stable/manpage.html) into a Python3 VirtualEnv.

[![Build Status](https://www.travis-ci.org/PyratLabs/ansible-role-sshuttle.svg?branch=master)](https://www.travis-ci.org/PyratLabs/ansible-role-sshuttle)

## Requirements

This role has been tested on Ansible 2.7.0+ against the following Linux Distributions:

  - Amazon Linux 2
  - CentOS 8
  - CentOS 7
  - Debian 10
  - Fedora 29
  - Fedora 30
  - Fedora 31
  - Ubuntu 18.04 LTS

## Disclaimer

If you have any problems please create a GitHub issue, I maintain this role in
my spare time so I cannot promise a speedy fix delivery.

## Role Variables


| Variable                           | Description                                                                  | Default Value        |
|------------------------------------|------------------------------------------------------------------------------|----------------------|
| `sshuttle_version`                 | Use a specific version of sshuttle, eg. `1.0.0`. Specify `false` for latest. | `false`              |
| `sshuttle_install_dir`             | Installation directory to put sshuttle virtual environments.                 | `$HOME/.virtualenvs` |
| `sshuttle_current_dirname`         | Name for the currently active sshuttle Virtualenv.                           | sshuttle             |
| `sshuttle_venv_site_packages`      | Allow venv to inherit packages from global site-packages.                    | `false`              |
| `sshuttle_install_venv_helper`     | Install a venv helper to launch venv executables from a "bin" directory.     | `true`               |
| `sshuttle_bin_dir`                 | "bin" directory to install venv-helpers to.                                  | `$HOME/bin`          |
| `sshuttle_install_os_dependencies` | Allow role to install OS dependencies.                                       | `false`              |
| `sshuttle_python3_path`            | Specify a path to a specific python version to use in virtualenv.            | _NULL_               |

## Dependencies

No dependencies on other roles.

## Example Playbook

Example playbook for installing to single user:

```yaml
- hosts: sshuttle_hosts
  roles:
     - { role: xanmanning.sshuttle, sshuttle_version: 1.0.0 }
```

Example playbook for installing the latest sshuttle version globally:

```yaml
---
- hosts: sshuttle_hosts
  become: true
  vars:
    sshuttle_install_os_dependencies: true
    sshuttle_install_dir: /opt/sshuttle/bin
    sshuttle_bin_dir: /usr/bin
    sshuttle_current_dirname: current
  roles:
    - role: xanmanning.sshuttle
```

### Activating the sshuttle venv

You need to activate the python3 virtual environment to be able to access `az`.
This is done as per the below:

```bash
source {{ sshuttle_install_dir }}/{{ sshuttle_current_dirname }}/bin/activate
```

In the above example global installation playbook, this would look like the
following:

```bash
source /opt/sshuttle/bin/current/bin/activate
```

## License

[BSD 3-clause](LICENSE.txt)

## Author Information

[Xan Manning](https://xanmanning.co.uk/)
