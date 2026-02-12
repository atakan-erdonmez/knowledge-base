- In permissions, there is two type: Absolute (777) and Symbolic (rwxrwxrwx)
- SUID: Execute program with it’s owners permissions (u+s)
- SGID: Execute program with it’s group permission & in directories, all subdirectories and files created inside will get the same group ownership regardless of creator (g+s)
- Sticky bit: Files with sticky bit can only be removed by root, owner or who have write permission on it.


