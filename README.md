# Ansible Sudo Role

[![Build Status](https://img.shields.io/travis/weareinteractive/ansible-sudo.svg)](https://travis-ci.org/weareinteractive/ansible-sudo)
[![Galaxy](http://img.shields.io/badge/galaxy-franklinkim.sudo-blue.svg)](https://galaxy.ansible.com/list#/roles/1380)
[![GitHub Tags](https://img.shields.io/github/tag/weareinteractive/ansible-sudo.svg)](https://github.com/weareinteractive/ansible-sudo)
[![GitHub Stars](https://img.shields.io/github/stars/weareinteractive/ansible-sudo.svg)](https://github.com/weareinteractive/ansible-sudo)

> `sudo` is an [ansible](http://www.ansible.com) role which:
>
> * installs sudo
> * configures sudo

## Installation

Using `ansible-galaxy`:

```
$ ansible-galaxy install franklinkim.sudo
```

Using `requirements.yml`:

```
- src: franklinkim.sudo
```

Using `git`:

```
$ git clone https://github.com/weareinteractive/ansible-sudo.git franklinkim.sudo
```

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```
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
#

# package name (version)
sudo_package: sudo
# list of username or %groupname
sudo_users: []
# list of username or %groupname and their defaults
sudo_defaults: []
```


## Example playbook

```
- host: all
  sudo: yes
  roles:
    - franklinkim.sudo
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
        users: 'user1,user2'
```

## Testing

```
$ git clone https://github.com/weareinteractive/ansible-sudo.git
$ cd ansible-sudo
$ vagrant up
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License
Copyright (c) We Are Interactive under the MIT license.
