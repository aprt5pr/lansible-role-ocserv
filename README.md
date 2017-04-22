# Ansible Role: Ocserv

[![Build Status](https://travis-ci.org/aprt5pr/lansible-role-ocserv.svg?branch=master)](https://travis-ci.org/aprt5pr/lansible-role-ocserv)

This role installs OpenConnect SSL VPN Server (ocserv).

### What is Ocserv?

Ocserv is an open source SSL VPN server. Check out https://gitlab.com/ocserv/ocserv for more info.

### Requirements

- Ansible >= 2.0

### Usage

NOTE: This role attempts to use sane defaults so that it can be run without needing to override any role default variables.

Assuming you'd like to execute Ansible from the same host that you'd like to install Ocserv on and you're on a RHEL-like distro, the steps are:
1. Install Ansible
```
$ sudo dnf install ansible # yum install ansible
```
2. Get the role from Ansible Galaxy
```
$ sudo ansible-galaxy install aprt5pr.ocserv
```
3. Update Ansible inventory
```
$ echo "127.0.0.1" | sudo tee -a /etc/ansible/hosts
```
4. Create a playbook
```
$ mkdir my-playbook
$ cd my-playbook
$ echo -e "---\n\n- hosts: all\n  roles:\n    - aprt5pr.ocserv" > site.yml
```
5. Run it!
```
$ ansible-playbook site.yml --become --ask-sudo-pass
```

If everything goes OK, you'll have Ocserv configured with a plain authentication user named `alice`.

### Gotchas
- This role (currently) does not:
   - Configure any source NAT. You'll need to configure this manually (e.g. `firewall-cmd --zone=public --add-masquerade`).
   - Manage the firewall - you may be unable to connect to the VPN remotely. The following should get you up and running:
     - `firewall-cmd --zone=public --add-port=443/tcp`
     - `firewall-cmd --zone=public --add-port=443/udp`

### How can I contribute code to this project?

- Fork this project
- Commit your changes
- Open a Merge Request
