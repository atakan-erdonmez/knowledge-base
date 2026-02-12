
When you change hostname with 
`hostnamectl set-hostname new_name`, you need to edit /etc/hosts file accordingly.

If not, sudo will try to resolve the new hostname, but won't due to security.


### Reason
The reason is:

### 🔒 `sudo` logs the command with your **hostname**

When you run a `sudo` command, it:

1. Resolves the **current hostname** to an IP (using `/etc/hosts` or DNS),
    
2. Logs the command like this:

    `Aug 4 12:00:00 maindebian sudo:  user : TTY=... ; COMMAND=...`


If the system can't resolve the hostname to an IP, it prints:

`sudo: unable to resolve host maindebian: Name or service not known`

---

### 🧠 Why the resolution fails:

When you changed the hostname (e.g., from `ubuntu` to `maindebian`), you **didn't update `/etc/hosts`**, which still contains:

`127.0.1.1    ubuntu`

So now, when `sudo` looks up `maindebian`, it doesn't exist in `/etc/hosts`, and DNS isn't used for local hostnames like this — hence the error.

---

### ✅ Moral of the story:

`sudo` relies on the hostname → `/etc/hosts` must map that hostname to an IP (usually `127.0.1.1`).