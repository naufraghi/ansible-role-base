# Ansible Base Role

_My first five minutes on a server_

[![License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](http://choosealicense.com/licenses/mit/)

--------------------------------------------------------------------------------

This is a basic Ansible role which implements almost everything described on [My First 5 Minutes On
A Server; Or, Essential Security for Linux
Servers](http://plusbryan.com/my-first-5-minutes-on-a-server-or-essential-security-for-linux-servers),
doing the following:

* Change the APT sources configuration to automatically use the nearest mirror;
* Update the system;
* Install some commonly used utilities such as `byobu`, `fish`, `iotop`, `htop`, `iftop`, `mosh`,
  etc;
* Enable the UFW firewall:
  - Sets the default policy to deny incoming packets;
  - Enable logging;
  - Allow SSH access only from certain network blocks (by default all IPv4 address space is allowed
    but setting the `ssh_allowed_networks` variable is highly recommended);
* Create a `deploy` user with a password of your choice;
  - Add an SSH key for remote login;
  - Allow the use of `sudo`;
* Lock down SSH:
  - Disable login for the `root` user;
  - Disable password-based authentication;
* Install and enable [fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page);
* Enable automatic installation of security updates.

This role is currently meant to be run as the first thing in your playbook and currently supports
only Ubuntu 14.04. Support for other Ubuntu versions or Linux distributions isn't planned at the
moment and may be rejected.


## Usage

A minimal playbook which makes use of this role is the following:

```yaml
---
- hosts: all
  sudo: yes
  roles:
  - role: base
    ssh_allowed_networks:
      - 2.228.72.0/26
      - 151.0.0.0/8
    deploy_authorized_key: "" # Put an SSH public key here
    deploy_password: "" # Put an encrypted password here
```
