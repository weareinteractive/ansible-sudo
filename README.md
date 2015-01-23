# Ansible Sudo Role

[![Build Status](https://travis-ci.org/weareinteractive/ansible-sudo.png?branch=master)](https://travis-ci.org/weareinteractive/ansible-sudo)
[![Stories in Ready](https://badge.waffle.io/weareinteractive/ansible-sudo.svg?label=ready&title=Ready)](http://waffle.io/weareinteractive/ansible-sudo)

> `sudo` is an [ansible](http://www.ansible.com) role which:
>
> * installs sudo
> * configures sudo

## Installation

Using `ansible-galaxy`:

```
$ ansible-galaxy install franklinkim.sudo
```

Using `arm` ([Ansible Role Manager](https://github.com/mirskytech/ansible-role-manager/)):

```
$ arm install franklinkim.sudo
```

Using `git`:

```
$ git clone https://github.com/weareinteractive/ansible-sudo.git
```

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```
# sudo_users:
#  - { name: '%foo', nopasswd: yes }
#  - { name: 'bar', nopasswd: no }
#  - name: '%foo'
#    nopasswd: yes
#    commands: '/bin/ls'
#  - name: 'bar'
#    nopasswd: no
#    commands: '/bin/nano'
#  - name: '%foo'
#    nopasswd: yes
#    commands: '/bin/nano /etc/hosts'

# list of username or %groupname
sudo_users: []
```

## Example playbook

```
- host: all
  roles:
    - franklinkim.sudo
  vars:
    sudo_users:
      - { name: 'foo', nopasswd: no }
      - { name: '%sudo', nopasswd: yes }
      - name: '%foo'
        nopasswd: yes
        commands: '/bin/ls'
      - name: 'bar'
        nopasswd: no
        commands: '/bin/nano'
      - name: '%foo'
        nopasswd: yes
        commands: '/bin/nano /etc/hosts'
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
