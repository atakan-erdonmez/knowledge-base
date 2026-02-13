Play: List of tasks that are being executed against a host 
Playbook: List of plays executed
Name: Name of the project
Hosts:
Tasks: What you  need to accomplish
Instruction
Parameters: What tool you are going to use

# Playbooks
Playbooks are files that lists the plays (tasks)

`ansible-playbook my_playbook.yml`

### Example Playbook
```
---
  - name: Name of the play
    hosts:   # Group of hosts
    tasks:
      - name: Name of the tasks (install htop)
        apt:
          name: htop
          state: latest
```


## Keywords
They are key-value pairs that changes the way task, play and other things to run.

**become: true**: Means become root when you are running this task
**when: ansible_facts.services\['nginx.service'].state == 'running'** -> Only run when this state is True
**gather_facts: yes** -> Ansible will gather system info on hosts you are working with

# Installation
- RedHat: `sudo dnf install epel-release && sudo dnf install ansible`

Location: `/etc/ansible`

## Hosts File
In hosts file, you can add hosts like this:
```
[db_servers]
server1
192.168.10.20

[db_servers:vars]
ansible_user=admin
ansible_password=MyPassword
```

This creates a group 'db_servers' and defines user-password to them

# Basic Commands
- `ansile db_servers -m ping` -> -m means module
- `ansible db_servers -a "reboot"` - > specify group and push ad-hoc command

