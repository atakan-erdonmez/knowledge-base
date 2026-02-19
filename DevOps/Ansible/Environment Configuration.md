Priority of config files:
1. Specified file on ENV ($ANSIBLE_CONFIG=/opt/ansible-web.cfg)
2. Config file in the same directory with playbook
3. User's home directoroy .ansible.cfg
4. Global /etc/ansible/ansible.cfg

`ansible-config list`: List all configuration
`ansible-config view`: Shows the current config file
`ansible-config dump`: Shows the current settings that are applied with source info