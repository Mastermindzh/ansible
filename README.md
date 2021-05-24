# ansible

Managed collection of ansible scripts to set up different services and automations.

## why?

I've used Ansible for a considerable amount of time now to manage most of my servers (or vms on ProxMox.. whatever :) ).
I've never really made my playbooks or configs public, but I've been sharing stuff left and right to people in need.
After a while I got thinking, why not just do what I do with most stuff... put it on Github so I can simply point people in the right direction!
So that's (part of) why this repo exists... it contains a few generic playbooks and a decent (i.m.o) starter setup.
I will add more over time, probably on request though.

## Table of contents

<!-- toc -->

- [directory structure](#directory-structure)
- [adding a new host to ansible](#adding-a-new-host-to-ansible)

<!-- tocstop -->

## directory structure

```sh
.
├── collections
├── inventory
│   └── hosts.yml # main ansible hosts file
├── logs # stores ansible logs
├── playbooks
│   ├── setup # ansible files only used when setting up a new server
│   └── ubuntu # ubuntu specific playbooks
├── roles
├── templates # all files replaced on hosts
│   └── timesyncd.conf
├── .ansible-lint # configuration for ansible-linter
├── ansible.cfg # configuration for ansible
├── package.json # main project file, contains run tasks and other niceties (husky / lint-staged)
└── README.md
```

## adding a new host to ansible

These are the steps to add a BRAND new (fresh install) host to your ansible inventory

1. set up a static ip / hostname for the target machine
    For Ubuntu:

    ```sh
      sudo nano /etc/netplan/50-cloud-init.yaml
    ```

    Now simply change it so it uses a static ip (use spaces.. cause yml):

    ```yml
      network:
        ethernets:
            eth0:
              dhcp4: true # keep using DHCP for nameservers
              addresses:
                - 10.10.1.3/24
              gateway4: 10.10.1.1
        version: 2
    ```

2. add ip / hostname to the inventory file
3. create a sudo user to execute playbooks as

    ```sh
      adduser username
      usermod -aG sudo username
    ```

4. add your ssh key to /home/username/.ssh/authorized_keys

    ``` sh
      ssh-import-id gh:username #imports from github on Ubuntu systems
    ```

5. Disable password-based logins

    ```sh
      sed "s/PasswordAuthentication.*/PasswordAuthentication no/g" /etc/ssh/sshd_config > /etc/ssh/sshd_config
    ```

6. Make sure python is installed
7. restart ssh

    ```sh
      sudo systemctl reload ssh
    ```

8. test...

      ```sh
        ansible ip/hostname -m ping
      ```
