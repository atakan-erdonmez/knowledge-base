![[disk1.png]]
Disk partitioning is dividing a hard drive into multiple logical storage units.

**Partitioning schemes:** How to partition disk, how many partitions can be, sizes, locations etc. are determined by partition schemes (GPT & MBR)

mount -a : mount everything in /etc/fstab file (without the ones with noauto)



# MBR

An old technology (1982). Compatible with old hardware and software.

- Uses BIOS

<aside> 💾 **Disk label type: dos (in fdisk)**

</aside>

- Supports maximum 4 primary partitions. You can create 3 primary and 1 extended partition and with logical partitioning, you can create a maximum of 15 partitions.


- Disk partitions are limited to 2TB.
- Uses 32 bits for storing logical block addresses and size information.

Note: An OS can not be installed on logical drive.

- First few sectors of a disk is always reserved. It is for OS to understand that where it will write data on disk.

---

<aside> 💾 In MBR, first 2048 bytes of a disk is reserved. There are four sector in reserved part:

</aside>

1. Sector: MBR (512 bytes)
    
    1. Boot sector (446 bytes)
    2. Partition sector (64 bytes)
    3. Magic number, The magic number serves as a validation check of the MBR. If it is a valid MBR, value is AA55. If value is different, disk is corrupt. (2 byte)
2. Sector: LVM (512 bytes)
    
3. Sector: LVM Metadata (512 bytes)
    
4. Sector: Metadata backup (512 bytes)
    

---

# GPT


Stands for “GUID Partition Table”. A newer technology. Address many of the limitations that the old MBR-based scheme imposes.

- Uses UEFI. GPT is a part of UEFI standard.
- Support maximum 128 partitions
- Allocates 64 bits for logical block addresses. This allows a GPT to accommodate partitions and disks size up to eight zebibytes (ZiB).
- Uses a GUID (globally unique identifier) to identify each disk and partition.
- In contrast to MBR, which has a single point of failure, GPT offers redundancy of its partition table information.
- GPT uses a checksum to detect errors and corruptions in the GPT header and partition table.

**Note:** In MBR, if MBR sector in the head of the disk corrupt, there is no way to recover. But in GPT, primary GPT resides at the head of the disk, while a backup copy, the secondary GPT, is housed at the end of the disk.

<aside> 💾 **Disk label type: gpt (in fdisk)**

</aside>

**udevadm:** The udevadm command ****is a device management tool in Linux which manages all the device events and controls the **udevd** daemon.

udevadm settle: After partitioning, this command tells kernel to update itself for hardware changes using udevd daemon



# Storage Protocols & Interfaces

| Interface | Protocol | Linux Device | SCSI-based? | Use Case              |
| --------- | -------- | ------------ | ----------- | --------------------- |
| SATA      | SATA     | /dev/sdX     | Indirectly  | Consumer HDD/SSD      |
| SAS       | SCSI     | /dev/sdX     | Yes         | Enterprise storage    |
| NVMe      | NVMe     | /dev/nvmeXnY | No          | High-performance SSDs |
| iSCSI     | SCSI/IP  | /dev/sdX     | Yes         | Network block storage |
| USB       | USB/UAS  | /dev/sdX     | Indirectly  | External drives       |
