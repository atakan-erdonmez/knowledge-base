# **LXC** (Linux Containers)

- **Low-level** container technology (like `chroot` on steroids).
    
- Gives you lightweight, **OS-level virtualization**.
    
- Each container shares the host kernel but feels like a separate Linux system.
    
- Used by developers and sysadmins for isolated environments.
    

# **LXD**

- **High-level manager** for LXC.
    
- Adds easier commands, image management, networking, snapshots, profiles, etc.
    
- Makes LXC containers usable like lightweight VMs.
    

> Think of:  
> **LXC = engine**  
> **LXD = friendly dashboard + tools on top**

---

# 🔧 How Does It Work?

- Containers run isolated processes with their own **filesystem**, **network**, **users**, and optionally **IP addresses**.
    
- **Host kernel is shared**, but containers think they're full systems.
    
- **No hardware emulation**, so it’s fast and efficient — perfect for RPi.
    

---

## ⚙️ LXD System Structure

- **Containers**: lightweight full Linux systems (Ubuntu, Debian, etc.)
    
- **Images**: base OS templates (from https://images.linuxcontainers.org/)
    
- **Storage Pools**: where containers live (e.g., `dir`, `zfs`)
    
- **Networks**: bridge for containers (usually `lxdbr0`)
    
- **Profiles**: reusable configs (network, storage, etc.)


# 📥 Installation (on Raspberry Pi OS or Debian-based systems)

```
sudo apt install snapd 
sudo snap install lxd 
sudo lxd init
```




---

## ✅ Initial Setup (`lxd init`)

Key prompts:

- Storage backend: use `dir` (simple)
    
- Network bridge: usually `lxdbr0` (isolates containers, gives NAT internet access)
    
- Remote images: yes
    
- IPv6: your choice (you can say no)
    

---

## 🔑 Common LXD Commands

### 🔹 Images
```
lxc image list ubuntu:       # See available OS images
lxc launch images:ubuntu/22.04 mycontainer
```
>To start your first container, try: lxc launch ubuntu:22.04
   Or for a virtual machine: lxc launch ubuntu:22.04 --vm

### 🔹 Container Management
```
lxc list                     # Show running containers
lxc launch ubuntu:22.04 lab1  # Create and start a container
lxc exec lab1 -- bash         # Shell into container
lxc stop lab1
lxc start lab1
lxc delete lab1
```

### 🔹 Snapshot & Restore
```
lxc snapshot lab1 clean
lxc restore lab1 clean
```

### 🔹 Filesystem
```
lxc file push file.txt lab1/tmp/   # Upload
lxc file pull lab1/tmp/file.txt .  # Download
```

### 🔹 Network
```
lxc network list
lxc network show lxdbr0
```
### 🔹 Profiles
```
lxc profile list
lxc profile show default
```

### 🔹 Locations
```
/var/lib/lxd/
```


## 🔑 Common LXC Commands

### To install a specific distro:
1. Check https://images.linuxcontainers.org to specify
2. Run `sudo apt install lxc-templates`
3. Run `sudo lxc-create -n name -t download`
4. Answer the questions (fedora, 42, arm64)
### To remove lxc container:
`sudo lxc-destroy -n lxc-fedora`
### List lxc containers
`lxs-ls`