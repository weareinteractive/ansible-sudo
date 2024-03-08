# Ansible axemann.sudo role

[![Build Status](https://img.shields.io/travis/com/axemann/ansible-role-sudo.svg)](https://travis-ci.org/axemann/ansible-role-sudo)
[![Galaxy](https://img.shields.io/badge/galaxy-axemann.sudo-blue.svg)](https://galaxy.ansible.com/ui/standalone/namespaces/13554)
[![GitHub Tags](https://img.shields.io/github/tag/axemann/ansible-role-sudo.svg)](https://github.com/axemann/ansible-role-sudo)
[![GitHub Stars](https://img.shields.io/github/stars/axemann/ansible-role-sudo.svg)](https://github.com/axemann/ansible-role-sudo)

> `axemann.sudo` is an [Ansible](http://www.ansible.com) role which:
>
> * installs sudo
> * configures sudo

**Note:**

> Since Ansible Galaxy supports [organization](https://www.ansible.com/blog/ansible-galaxy-2-release) now, this role has moved from `franklinkim.sudo` to `axemann.sudo`!

## Installation

Using `ansible-galaxy`:

```shell
ansible-galaxy install axemann.sudo
```

Using `requirements.yml`:

```yaml
- src: axemann.sudo
```

Using `git`:

```shell
git clone https://github.com/axemann/ansible-role-sudo.git axemann.sudo
```

## Dependencies

* Ansible >= 2.5

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```yaml
---
# sudo_defaults:
#  - defaults: env_reset
#  - name: user1
#    defaults: requiretty
# sudo_users:
#  - name: '%group1'
#  - name: 'bar'
#    nopasswd: yes
#  - name: '%group2'
#    commands: '/bin/ls'
#  - name: '%group3'
#    commands:
#      - /bin/ls
#      - /bin/df
#  - name: '%group4'
#    hosts: 127.0.0.1

# package name (version)
sudo_package: sudo
# list of username or %groupname
sudo_users: []
# list of username or %groupname and their defaults
sudo_defaults: []
# default sudoers file
sudo_sudoers_file: ansible
# path of the sudoers.d directory
sudo_sudoers_d_path: /etc/sudoers.d
# delete other files in `sudo_sudoers_d_path`
purge_other_sudoers_files: false

```

## Usage

This is an example playbook:

```yaml
---

- hosts: all
  become: yes
  roles:
    - axemann.sudo
  vars:
    sudo_defaults:
      - defaults: env_reset
      - defaults: secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
      - name: 'user1'
        defaults: 'requiretty'
      - name: '%group1'
        defaults: '!requiretty'
    sudo_users:
      - name: 'user1'
      - name: 'user2'
        nopasswd: yes
      - name: '%group1'
        hosts: 127.0.0.1
      - name: '%group2'
        commands: '/bin/ls'
      - name: '%group3'
        commands:
          - '/usr/bin/ls'
          - '/usr/bin/df'
          - '/usr/bin/mailq'
      - name: '%group4'
        users: 'user1,user2'
        groups: 'group1,group2'
    purge_other_sudoers_files: yes

```

## Testing

```shell
git clone https://github.com/axemann/ansible-role-sudo.git
cd ansible-role-sudo
make test
```

## Contributing

In lieu of a formal style guide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

*Note: To update the `README.md` file please install and run `ansible-role`:*

```shell
gem install ansible-role
ansible-role docgen
```

## License

Copyright (c)  under the MIT license.
