#### Securing LXC

Let us limit the resources to the container. In order to configure `cgroups` for LXC and limit the CPU and memory, a container can create a new configuration file in the `/usr/share/lxc/config/<container name>.conf` directory with the name of our container. For example, to create a configuration file for a container named `linuxcontainer`, we can use the following command:

```shell-session
ataker@htb[/htb]$ sudo vim /usr/share/lxc/config/linuxcontainer.conf
```

In this configuration file, we can add the following lines to limit the CPU and memory the container can use.

```txt
lxc.cgroup.cpu.shares = 512
lxc.cgroup.memory.limit_in_bytes = 512M
```

When working with containers, it is important to understand the `lxc.cgroup.cpu.shares` parameter. This parameter determines the CPU time a container can use in relation to the other containers on the system. By default, this value is set to 1024, meaning the container can use up to its fair share of CPU time. However, if we set this value to 512, for example, the container can only use half of the CPU time available on the system. This can be a useful way to manage resources and ensure all containers have the necessary access to CPU time.

One of the key parameters in controlling the resource allocation of a container is the `lxc.cgroup.memory.limit_in_bytes` parameter. This parameter allows you to set the maximum amount of memory a container can use. It's important to note that this value can be specified in a variety of units, including bytes, kilobytes (K), megabytes (M), gigabytes (G), or terabytes (T), allowing for a high degree of granularity in defining container resource limits. After adding these two lines, we can save and close the file. To apply these changes, we must restart the LXC service.

```shell-session
ataker@htb[/htb]$ sudo systemctl restart lxc.service
```

LXC use `namespaces` to provide an isolated environment for processes, networks, and file systems from the host system. Namespaces are a feature of the Linux kernel that allows for creating isolated environments by providing an abstraction of system resources.

Namespaces are a crucial aspect of containerization as they provide a high degree of isolation for the container's processes, network interfaces, routing tables, and firewall rules. Each container is allocated a unique process ID (`pid`) number space, isolated from the host system's process IDs. This ensures that the container's processes cannot interfere with the host system's processes, enhancing system stability and reliability. Additionally, each container has its own network interfaces (`net`), routing tables, and firewall rules, which are completely separate from the host system's network interfaces. Any network-related activity within the container is cordoned off from the host system's network, providing an extra layer of network security.

Moreover, containers come with their own root file system (`mnt`), which is entirely different from the host system's root file system. This separation between the two ensures that any changes or modifications made within the container's file system do not affect the host system's file system. However, it is important to remember that while namespaces provide a high level of isolation, they do not provide complete security. Therefore, it is always advisable to implement additional security measures to further protect the container and the host system from potential security breaches.

Here are 9 optional exercises to practice LXC:

|     |                                                                                                        |
| --- | ------------------------------------------------------------------------------------------------------ |
| 1   | Install LXC on your machine and create your first container.                                           |
| 2   | Configure the network settings for your LXC container.                                                 |
| 3   | Create a custom LXC image and use it to launch a new container.                                        |
| 4   | Configure resource limits for your LXC containers (CPU, memory, disk space).                           |
| 5   | Explore the `lxc-*` commands for managing containers.                                                  |
| 6   | Use LXC to create a container running a specific version of a web server (e.g., Apache, Nginx).        |
| 7   | Configure SSH access to your LXC containers and connect to them remotely.                              |
| 8   | Create a container with persistence, so changes made to the container are saved and can be reused.     |
| 9   | Use LXC to test software in a controlled environment, such as a vulnerable web application or malware. |


## Related

- [[SSH Hardening]]