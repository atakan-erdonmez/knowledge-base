1. Boot from the CD via BIOS
2. Select "Troubleshooting" and start in "[[Linux Starting Modes#Rescue Mode|Rescue Mode]]"
3. Mount the system
4. `chroot /mnt/sysimage`
5. `passwd root`

To prevent this, put a BIOS password