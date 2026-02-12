When you boot to proxmox, it creates 2 parts in your SSD:
Local
Local-lvm

Local is for backups, ISOs, and templates. It is mounted in /var/lib/vz
Local-lvm is **thin lvm provizion** used for VM files.

> [!NOTE] 
> When installing Windows, add VirtIO drivers as CD/ROM. Download from here
> [Link](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbDBiTk0tUEhBd1l5aFVnOVI5YW9Qekk3aEVkd3xBQ3Jtc0tuMVZNc3dnUmlBSWk4T0dicl9KM2lSTlc5MGx2UHdvd2toVVZQTXVydVVzUEJlVTNjQmxnN1hONVpvcm02b0FSR2hOUmdtN1I3NnBSSUdjQWF5dnBkZUp0SHlfTW55SnZLRDlreVRwUXFRNnF1NmlqTQ&q=https%3A%2F%2Flearnlinux.link%2Fvirt-win&v=eyNlGAzf-L4)
> You might need to find the correct HDD drive in vioscsi. You can also install missing drivers in Device Manager via selecting the CD/DVD.
# Installation
## System
For any modern Linux distro, suggestions are :
- **Graphic card**: Default / VirtIO-GUP
- **Machine**: q35 (UEFI) (i440fx is much older chipset that uses BIOS)
- **BIOS**: OVMF 
- **SCSI Controller**: VirtIO SCSI (LSI 53C895A is old VirtIO SCSI Single is for single threaded stuff, other are niche)
## Disks
- **Bus**: SCSI (VirtIO SCSI is best, IDE is slow&old, SATA is for compatible but not as strong)
- **Cache**: Default is for guest operating systems cache, write through is for Proxmox's physical disk write, write back is for using RAM as cache, you don't have to wait
- **Discard**: Should be enabled for SSDs, since it sends TRIM to SSD when you delete something to mark as free, protecting SSD's health
- **IO Thread**: Can increase I/O performance via creating a new I/O thread. Not necessary if not a big database or file server.

> It is suggested to install `qemu-guest-agent` package
> Then enable `sudo systemctl qemu-guest-agent.service`
> Lastly, enable Qemu guest in settings

# Detailed explanations of startup settings
### 1. Deep Dive into VM Creation Settings

#### 1.1 System Tab

- **Graphic Card (GPU):** Defines the virtual display adapter.
    
    - **`VirtIO-GPU`:** (Recommended Default) Highest performance, requires modern guest OS with VirtIO drivers (built into most Linux distros).
        
    - **`Standard VGA`:** Maximum compatibility for older or problematic operating systems, but with basic performance.
        
- **Machine Type:** Defines the virtual motherboard chipset.
    
    - **`Q35`:** (Recommended Default) Modern chipset with PCIe support. Required for advanced features like GPU passthrough. Use for all modern operating systems.
        
    - **`i440FX`:** Older chipset for compatibility with legacy operating systems.
        
- **BIOS:** Defines the firmware.
    
    - **`OVMF (UEFI)`:** (Recommended) Modern UEFI firmware. Required for Secure Boot and Windows 11.
        
    - **`SeaBIOS`:** Traditional BIOS firmware for broad compatibility.
        
- **SCSI Controller:** Defines the controller for `SCSI` type disks.
    
    - **`VirtIO SCSI`:** (Recommended Default) Highest performance paravirtualized controller. Best choice for all modern Linux VMs and Windows with drivers.
        
    - **`VMware PVSCSI`:** High-performance option used for compatibility when migrating VMs from VMware.
        
    - **`LSI / MegaRAID`:** Emulated hardware controllers for compatibility with legacy systems or specific software that requires them.
        

#### 1.2 Disks Tab

- **Bus / Device:** Defines how the disk is connected.
    
    - **`SCSI`:** (Recommended) Connects the disk to the controller chosen on the System tab (ideally `VirtIO SCSI`).
        
    - **`VirtIO Block`:** An alternative high-performance paravirtualized option. `VirtIO SCSI` is generally more flexible.
        
    - **`SATA`:** Emulates a standard SATA drive. Good for Windows without loading special drivers.
        
    - **`IDE`:** Slowest option, for legacy OS compatibility only.
        
- **Cache:** Defines how the host uses RAM to cache disk operations.
    
    - **`No cache`:** (Safe Default) Relies on the guest OS's own caching. Good, reliable performance.
        
    - **`Write back`:** (Highest Performance, Unsafe) Host reports writes as complete instantly. **Risk of data loss on power failure unless you have a UPS.**
        
    - **`Write through`:** (Safest) Host reports writes as complete only after data is on the physical disk. Slower write performance.
        
- **Discard (TRIM):** **Check this box.** This allows the VM to tell the SSD and `local-lvm` storage which blocks are free, reclaiming space and maintaining SSD health.
    
- **IO Thread:** Check this box for a potential performance boost on I/O-heavy VMs (like databases) when using a `VirtIO` disk.
    



#### 1.3 Disks Tab (Advanced Options)

- **SSD Emulation:** A flag to make a disk report itself as an SSD to the guest OS. This is generally **not needed** when using a real SSD with the `VirtIO SCSI` driver. Just use the `Discard` option.
    
- **Async IO (AIO):** The low-level API for disk I/O.
    
    - **`io_uring`:** (Recommended Default) The most modern, high-performance API in the Linux kernel.
        

#### 1.4 CPU Tab

- **Sockets vs. Cores:**
    
    - **Sockets:** Number of virtual CPU sockets presented to the guest.
        
    - **Cores:** Number of cores per socket.
        
    - **Total vCPUs = Sockets x Cores**.
        
    - **Recommendation:** For best compatibility and to avoid potential software licensing issues, always use **1 Socket** and set the `Cores` value to the number of virtual cores you need.
        
- **CPU Type:**
    
    - **`host`:** (Recommended for single-node setups) Passes your actual CPU model and all its features/instruction sets to the VM. This provides the best performance.
        
    - **`kvm64`:** A generic, highly compatible CPU model. Use this if you plan to live-migrate VMs between hosts with different physical CPUs.
        
- **Greyed-Out Options:**
    
    - **`VCPUs`:** This is always greyed out because it's a calculated field that displays `Sockets x Cores`.
        
    - **`CPU limit` & `CPU affinity`:** These are advanced resource control settings that are only configurable _after_ a VM has been created (under the Hardware tab, by editing the "Processors" entry).

##### CPU Type Detailed
|Setting|What it does|Pick it when…|
|---|---|---|
|**host**|Passes your real CPU’s full feature set straight through. Fastest.|You will _never_ live-migrate this VM to a different machine. (Best choice for a standalone template on one box.)|
|**kvm64 / qemu64**|Very old, ultra-compatible “generic” CPUs with almost no modern instructions. Slow.|Only if you must guarantee that a VM boots on _any_ random x86 host, even Pentium-era. Almost never needed today.|
|**Named models (Skylake-Server, Cascadelake, EPYC-Rome, etc.)**|Emulates that exact micro-architecture’s instruction set. Gives you AVX/AVX2, AES-NI, etc.|You run a cluster and want live-migration; pick the newest model that **all** nodes support.|
|**x86-64-v1/v2/v3/v4 (-aes)**|Generic “levels” standardized by QEMU:  <br>• **v1:** SSE2 baseline  <br>• **v2:** +SSE3/SSSE3/SSE4.1/4.2  <br>• **v3:** +AVX/AVX2/F16C, etc.  <br>• **v4:** +AVX-512, SHA, GFNI…  <br>The “-aes” suffix simply adds AES-NI even if some very old CPUs lacked it.|Good middle-ground for mixed hardware when you don’t want to think of brand names. **“x86-64-v2-aes”** (the Proxmox default) works on any CPU from roughly 2010 onward.|
|**max**|At start-up QEMU exposes “the highest common feature set of all nodes in the cluster” automatically.|You have a heterogeneous Proxmox cluster and keep it updated; want migration without micro-managing models.|

**Vendor field**

_Just the ID string the guest sees (`GenuineIntel`, `AuthenticAMD`, etc.)._  
It matters only for a few license checkers (e.g., SQL Server wants an “Intel” string). Leave it on **default** unless a guest application complains.

---

###### What to choose for a _template_ on a single Proxmox host

| Scenario                                                 | Recommended CPU Type                                                                            |
| -------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| One physical server, no migration                        | **host** – maximum speed, no downsides.                                                         |
| Might add another similar server later but not identical | **x86-64-v3** (or keep the default **x86-64-v2-aes**) for wide compatibility while keeping AVX. |
| Mixed Intel + AMD cluster                                | **max** or explicitly set **x86-64-v2-aes** on every VM.                                        |

That’s it – keep it simple: **use “host” for single-box templates; leave the vendor on default.**


### 2. Post-Creation VM Management

#### Changing VM Settings

You can change most VM settings after creation, but some are easier than others. **The VM must be powered off to change hardware settings.**

- **Easy to Change:** (Select VM -> Hardware -> Select Device -> Edit)
    
    - Cache mode
        
    - Discard option
        
    - IO Thread option
        
- **Difficult/Risky to Change (for the Boot Disk):**
    
    - **Bus / Device:** Changing the bus type (e.g., from SATA to SCSI) for a disk that contains the operating system will likely break the VM's bootloader, as the OS will no longer be able to find its boot files. This requires an advanced rescue operation to fix. It's best to set this correctly at creation.
