# ansible

Managed collection of ansible scripts to set up different services and automations.

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
