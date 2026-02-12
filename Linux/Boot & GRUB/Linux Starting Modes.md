# Rescue Mode



In UEFI screen, press `e` to edit config. In the "linux" line, add this to the end:
`systemd.unit=rescue.target`

- This is single user mode
- In this mode, you can reset root password. [[Root Password Reset]]. To prevent this: [[GRUB Password Creation]]


