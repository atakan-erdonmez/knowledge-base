In order to define more complex permissions to files and directories, we should use ACLs (Access Control Lists). So we can define specific permission for users and group independently. It is shown with “+” sign at the end of the permission.

- getfacl: Show file’s ACL
    
- setfacl: Set file’s ACL
    
    - -m: modify
    - -x: remove
    - u: user g: group
    - -b: ??? (removing all ACL from file/directory)
    
    Usage: setfacl -m u:atakan:rw file
    

**Default ACL:** Default ACL is inherited in subdirectories. It is only given to directories. It uses -d option

-R : Recursive, must be used 

setfacl -d -Rm(recursive modify) u:atakan:rwx dir → makes all directories inside have rwx permission for atakan user