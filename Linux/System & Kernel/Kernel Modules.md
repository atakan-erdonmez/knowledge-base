lsmod: View loaded kernel modules

You can see the loaded modules in `/sys/module`. After you load modules, you can see them here. You can check the parameters folder in any module, too


> st is an example module

modinfo: Detail about the module
	`modinfo st`
mobprobe: Load the module
	`modprobe st`
modprobe -r: Unload the module
	`modprobe -r st`


`/lib/modules/<kernel_name>/kernel` -> you can find the kernel modules here in a categorized way


### Parameters
`modinfo -p` -> show parameters of a module
`modprobe -v st buffer_kbs=64` -> load the 'st' module with a parameter

##### Permanent parameter

In /etc/modprobe.d

```
vi st.conf
options st buffer_kbs=64 max_sg_segs=512
## specify options
```

then load with `modprobe -v st` (-v is verbose)