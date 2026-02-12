This enables putting a password for accessing GRUB
### 1. Generate a GRUB Password Hash

First, create an encrypted password hash. Open your terminal and run:

```
grub2-mkpasswd-pbkdf2
```

Enter your desired password twice. The command will output a long hash string that looks like `grub.pbkdf2.sha512.10000.E2...`. **Copy this entire string.**

### 2. Set the Superuser and Password

Next, you need to add a configuration file to tell GRUB to use this password. The safest method is to create a new file in `/etc/grub.d/` to avoid your changes being overwritten by system updates.


```
sudo nano /etc/grub.d/01_users
```

Paste the following content into the file. Replace `admin` with your desired username and paste the hash you copied in the previous step.

```
# Set a superuser and password for GRUB
cat << EOF
set superusers="admin"
password_pbkdf2 admin YOUR_COPIED_PASSWORD_HASH_HERE
EOF
```

Save the file and exit the editor (in `nano`, press `Ctrl+X`, then `Y`, then `Enter`).

Make the script executable:


```
sudo chmod +x /etc/grub.d/01_users
```

### 3. Update the GRUB Configuration

Finally, apply the changes to your GRUB configuration. The command differs based on your Linux distribution family.

- **On Debian/Ubuntu:**

```
sudo update-grub
```

- **On Fedora/RHEL/CentOS:**

```
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

### Restrict menu entries (optional but recommended)

To protect menu entries, add this after each menuentry in `/etc/grub.d/10_linux` or similar:


```
--unrestricted  # if you want a specific entry to stay open
```

Or remove `--unrestricted` if you want password protection for that entry

> You can remove it from the `/etc/grub.d/10_linux` file from the line starting with "CLASS"


