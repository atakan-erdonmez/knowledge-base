`sudo apt install corectrl` -> See and manage config of CPU&GPU

`sudo apt install glmark2` -> Use for 3D rendering for GPU testing

`sudo apt install radeontop` -> Shows live GPU usage in terminal


>[!Enable AMD GPU custom config]
>`/etc/default/grub` add:
> - amdgpu.ppfeaturemask=0xffffffff


