1. Go to edit mode in boot. [[Linux Starting Modes]]
2. In "linux" line, change `ro` with `rw rd.break`
3. In `switch_root` prompt, enter `mount` and check the rhel-root mount point (which should be /sysroot)
4. Re-mount with `mount -o remount,rw /sysroot` if not rw
5. chroot /sysroot
6. passwd

This will only work if there is no GRUB password