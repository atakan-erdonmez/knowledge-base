Playbook: A single YAML file
Play: defines a set of activities (tasks) to be run on hosts
Task: An action to be performed on the host
Module: The different actions run by tasks

- Execute playbook:
`ansible-playbook playbook.yaml`

# Verifying Playbooks
### Check Mode
Ansible executes "dry run" where no actual changes are made on hosts
`ansible-playbook install_nginx.yaml --check`

>[!note]
>Not all modules support check mode

### Diff Mode
Provides a before-and-after comparison of playbook changes. It is helpful to understand and verify the impact of playbook
`ansible-playbook install_nginx.yaml --check --diff`

### Syntax Check
Checks the syntax of the playbook
`ansible-playbook install_nginx.yaml --syntax-check`

## Ansible-lint
It is a tool to check complex playbooks for bugs, errors, stylistic errors, and suspicious constructurs.
`ansible-lint style_example.yaml`


## Conditions
![[Conditions]]