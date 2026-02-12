# qm
QEMU manager. Used for managing VMs

| Commands                                 | Action                                                               |
| ---------------------------------------- | -------------------------------------------------------------------- |
| qm list                                  | List VMs (will list templates too)                                   |
| qm config \<vm_id>                       | Show the config of VM (everything here can be set with set --option) |
| qm start \| shutdown \| reboot  \<vm_id> | Start/stop/reboot that VM (can't start templates)                    |
| qm reset \<vm_id>                        | Force reboot. Do not use if not necessary                            |
| qm stop \<vm_id>                         | Force shutdown. Do not us if not necessary                           |
| qm set --onboot 0 \| 1 \<vm_id>          | Set start at boot option                                             |
| qm set --memory 1024 \<vm_id>            | Set memory. Everything can be set in `qm config`                     |

# pct
Proxmox Container Toolkit. Used for managing containers

| Commands                        | Action                            |
| ------------------------------- | --------------------------------- |
| pct list                        | List container (templates too)    |
| pct config                      | Show details                      |
| pct start \| shutdown \| reboot | Container                         |
| pct enter \<ct_id>              | Login to the container to the CLI |
| pct set \<vm_id> -onboot 1      | 1 hypen                           |
