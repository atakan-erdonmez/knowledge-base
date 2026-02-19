Conditions are used in playbooks. There are modules that will help you. You can use most logic operators
## when
```
- name: install nginx on debian
  apt: 
	  name: nginx
	  state: present
  when: ansible_os_family == "Debian" or "Ubuntu"
```

You can also use 'ansible_facts':
`when: ansible_facts['os_family'] == "Debian" and ansible_facts['distribution_major_version'] == '18'`

## Conditionals in Loops
```
---
- name: Install Softwares
  hosts: all
  vars:
    packages:
      - name: nginx
        required: True
      - name: mysql
        required: True
      - name: apache
        required: False

  tasks:
    - name: Install "{{ item.name }}" on Debian
      apt:
        name: "{{ item.name }}"
        state: present
		when: item.required == True ######
      loop: "{{ packages }}"
```