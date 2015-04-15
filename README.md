# Ansible Base Role

_My first five minutes on a server_

[![License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](http://choosealicense.com/licenses/mit/)

--------------------------------------------------------------------------------

An Ansible role to setup some basics on Ubuntu and OS X machines. It implements almost everything
[My First 5 Minutes On A Server; Or, Essential Security for Linux
Servers](http://plusbryan.com/my-first-5-minutes-on-a-server-or-essential-security-for-linux-servers)
and sensibly changes some default packages and configurations depending on the platform.

This role currently supports:

- OS X 10.10
- Ubuntu 14.04

For more information, see the platform-specific sections below.


## OS X

This role performs the following:

* Install command line tools;
* Install [Homebrew](http://brew.sh);
* Install [Caskroom](http://caskroom.io);
* Enable the [Application Firewall](https://support.apple.com/en-us/HT201642);
* Disable root login via SSH;
* Disable password login via SSH;


## Ubuntu

On Ubuntu, this role performs the following:

* Change the APT sources configuration to automatically use the nearest mirror;
* Update the system;
* Install some commonly used utilities;
* Enable the UFW firewall, denying incoming packets, enabling logging and allowing SSH access only
  to some subnets.
* Create a `deploy` user with a password of your choice;
  - Add an SSH key for remote login;
  - Allow the use of `sudo`;
* Disable root login via SSH;
* Disable password login via SSH;
* Install and enable [fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page);
* Enable automatic installation of security updates.


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
    deploy_authorized_keys:
      - "" # Put an SSH public key here
    deploy_password: "" # Put an encrypted password here
```
