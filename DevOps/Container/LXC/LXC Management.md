| Command                                       | Description                                                    |
| --------------------------------------------- | -------------------------------------------------------------- |
| `lxc-ls`                                      | List all existing containers                                   |
| `lxc-stop -n <container>`                     | Stop a running container.                                      |
| `lxc-start -n <container>`                    | Start a stopped container.                                     |
| `lxc-restart -n <container>`                  | Restart a running container.                                   |
| `lxc-config -n <container name> -s storage`   | Manage container storage                                       |
| `lxc-config -n <container name> -s network`   | Manage container network settings                              |
| `lxc-config -n <container name> -s security`  | Manage container security settings                             |
| `lxc-attach -n <container>`                   | Connect to a container.                                        |
| `lxc-attach -n <container> -f /path/to/share` | Connect to a container and share a specific directory or file. |

