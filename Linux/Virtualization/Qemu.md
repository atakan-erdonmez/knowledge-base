Install (might be old, qemu-kvm package splitted): 
`sudo yum install qemu-kvm qemu-img virt-manager libvirt libvirt-python \libvirt-client virt-install virt-viewer bridge-utils`

Debian (new):
`sudo apt install qemu-system-x86 qemu-utils libvirt-daemon-system libvirt-clients virt-manager bridge-utils`

- `qemu-system-x86`: Main QEMU emulator for x86
- `qemu-utils`: Tools like `qemu-img`
- `libvirt-*`: For managing VMs
- `virt-manager`: Optional GUI
- `bridge-utils`: For bridged networking
