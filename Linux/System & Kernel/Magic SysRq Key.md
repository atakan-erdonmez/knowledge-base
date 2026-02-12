## 🔧 What is the **Magic SysRq Key**?

- It's a **kernel-level backdoor** for system recovery, debugging, and emergency control.
    
- SysRq = _System Request_. It's **built into the Linux kernel**.
    
- It allows you to send **raw commands directly to the kernel**, bypassing userland entirely.
    
- Works even when:
    
    - X server is frozen
        
    - TTYs are locked
        
    - Mouse/keyboard don't respond
        
    - Most of userspace is unresponsive
        

> 🧠 It does **not** require any running process — it interacts with the kernel directly.

---

## ⌨️ Where Is the SysRq Key?

- On most keyboards, it's **shared with the `Print Screen` key**.
    
- To use it, you usually hold:
    
```
Alt + SysRq (aka PrtSc) + [Command key]
```
    
- On laptops you might also need `Fn` to access it.
    

---

## 🧪 How It Works

SysRq commands are sent via:

```
Alt + SysRq + [command character]
```

The kernel listens for these key combos and performs hardcoded actions. It works as long as:

- The kernel is not totally dead (e.g., a hardware hang or kernel panic might block it).
    
- `/proc/sys/kernel/sysrq` is enabled.
    

---

## ✅ What is **REISUO**?

It's a **safe shutdown sequence** using Magic SysRq:

|Key|Meaning|Action|
|---|---|---|
|**R**|Raw|Take back control from userland (e.g., X)|
|**E**|Terminate|Send SIGTERM to all processes|
|**I**|Kill|Send SIGKILL to all processes|
|**S**|Sync|Flush all RAM data to disk|
|**U**|Unmount|Remount filesystems as read-only|
|**O**|Off|Power off (or use **B** for reboot)|

> 💡 It's like a **manual controlled shutdown** step-by-step.

Each step gives the system time to clean up before the next. This avoids corruption.

---

## 🔐 Is It Enabled?

Check:

```cat /proc/sys/kernel/sysrq
```

- `0` = disabled
    
- `1` = fully enabled
    
- Other numbers = partially enabled (bitmask)
    

Enable it:

```echo 1 | sudo tee /proc/sys/kernel/sysrq
```

Make permanent:

```echo "kernel.sysrq = 1" | sudo tee -a /etc/sysctl.conf sudo sysctl -p
```

---

## 🔍 What Are Other SysRq Commands?

Here are some useful ones:

|Key|Action|
|---|---|
|`R`|Switch keyboard from raw to XLATE (fixes input issues)|
|`E`|Send SIGTERM to all processes|
|`I`|Send SIGKILL to all processes|
|`S`|Sync all mounted filesystems|
|`U`|Remount all filesystems read-only|
|`O`|Shut down|
|`B`|Reboot immediately (no unmount/sync!)|
|`K`|Kill all processes on the current TTY (like a local panic)|
|`M`|Dump memory info to console|
|`T`|Dump process list|
|`P`|Dump current registers and flags|
|`G`|Trigger crash dump if configured|

---

## 🧠 When Should You Use It?

Use Magic SysRq when:

- System is **hard-locked or frozen**
    
- You cannot access TTY (Ctrl+Alt+F3, etc.)
    
- SSH isn't working
    
- You want to **force a clean shutdown without power cycling**
    

Avoid just holding the power button, which **risks data loss**.