````
# Samba Configuration Guide & Troubleshooting

## 1. Core Concept

Samba is a service that allows a Linux server to speak the SMB/CIFS protocol. It makes your Linux machine appear as a native Windows file/print server on the network.

---

## 2. Installation

### On Fedora / RHEL
```bash
sudo dnf install samba samba-client samba-common
````

### On Debian / Ubuntu

Bash

```
sudo apt install samba
```

---

## 3. Configuration File: `/etc/samba/smb.conf`

This file controls the entire Samba server's behavior. It's made of sections.

### `[global]` Section (Server-wide settings)

- `workgroup = WORKGROUP` : Your network's workgroup name.
- `security = user` : Requires users to have a valid Samba username/password.
- `server string = My Fedora Server` : A descriptive name.
- `map to guest = bad user` : Needed for guest/anonymous access to work.

### Share Definition Section (e.g., `[MyShare]`)

This defines a specific folder you want to share.

- `path = /srv/samba/myshare` : Absolute path to the folder on your Linux system.
- `comment = A descriptive comment`
- `browseable = yes` : Makes the share visible on the network.
- `writable = yes` or `read only = no` : Allows users to write files.
- `guest ok = yes` : Allows anonymous access (no password needed).
- `valid users = user1, user2, @groupname` : Restricts access to only these users/groups.

---

## 4. User Management

Samba has its own password database, separate from the main Linux system.

- **Rule:** A user **must exist in Linux first** before they can be a Samba user.
- **Command:** `smbpasswd` is the tool to manage this database.
    - `sudo smbpasswd -a <username>` : **A**dds a Linux user to Samba and sets their password.
    - `sudo smbpasswd -x <username>` : **Deletes** a user from Samba.

---

## 5. The 3 Layers of Permissions (Troubleshooting Checklist)

For a user to access a share, they must pass through **ALL THREE** of these security gates. If access is denied, check them in this order.

### 🥇 Layer 1: Filesystem Permissions (The Building Key)

Does the user have basic Linux rights to the folder?

- **Check with:** `ls -ld /path/to/share`
- **Problem:** The user Samba logs in as (e.g., `atakan` or `nobody` for guests) doesn't own the file or have read/write/execute permissions.
- **Fix:** Use `chown` to set ownership and `chmod` to set permissions.
    
    Bash
    
    ```
    # Example for a user's share
    sudo chown -R atakan:atakan /path/to/share
    sudo chmod -R 775 /path/to/share
    ```
    

### 🥈 Layer 2: Samba Authentication (The Security Desk ID)

Does the user have a valid Samba password? (Not required for `guest ok = yes` shares).

- **Problem:** The user exists in Linux but has no Samba password set.
- **Fix:** Add the user to the Samba database.
    
    Bash
    
    ```
    sudo smbpasswd -a atakan
    ```
    

### 🥉 Layer 3: Samba Share Authorization (The VIP Room List)

Is the user explicitly allowed to access this specific share?

- **Check:** The `valid users` line in your `smb.conf` for that share.
- **Problem:** The `valid users` parameter exists, but the user trying to connect is not on the list.
- **Fix:** Add the user to the `valid users` line or remove the line entirely to allow any authenticated user.

#### ★ Special Layer for Fedora/RHEL: SELinux Context

This is a bonus gatekeeper on Fedora. If you get `Permission Denied` and everything else seems right, it's almost always SELinux.

- **Check with:** `ls -ldZ /path/to/share`
- **Problem:** The context is not `samba_share_t`.
- **Fix (Permanent):**
    
    Bash
    
    ```
    sudo semanage fcontext -a -t samba_share_t "/path/to/share(/.*)?"
    sudo restorecon -Rv /path/to/share
    ```