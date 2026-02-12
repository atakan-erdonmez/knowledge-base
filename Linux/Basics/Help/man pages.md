To search for a manual page by keyword, use the -k option:
`man -k keyword`

This is helpful if you don’t quite know the name of the command that you want. For example, if you’re looking for a command to sort something, run:
```
$ man -k sort
--snip-- 
comm (1) - compare two sorted files line by line 
qsort (3) - sorts an array 
sort (1) - sort lines of text files 
sortm (1) - sort messages 
tsort (1) - perform topological sort 
--snip--
```


The output includes the manual page name, the manual section (see below), and a quick description of what the manual page contains. 

> NOTE If you have any questions about the commands described in the previous sections, you may be able to find the answers by using the man command. 

Manual pages are referenced by numbered sections. When someone refers to a manual page, they often put the section number in parentheses next to the name, like ping(8). Table 2-3 lists the sections and their numbers.

### Online Manual Sections 

| Section | Description                                                        |
|---------|--------------------------------------------------|
| 1       | User commands                                                      |
| 2       | Kernel system calls                                                |
| 3       | Higher-level Unix programming library documentation                |
| 4       | Device interface and driver information                            |
| 5       | File descriptions (system configuration files)                     |
| 6       | Games                                                              |
| 7       | File formats, conventions, and encodings (ASCII, suffixes, and so on) |
| 8       | System commands and servers                                        |
