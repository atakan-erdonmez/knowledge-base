Net user: allows us to display a list of all users on a host, information about a specific user, and to create or delete users.

#### Net Group / Localgroup

[Net Group](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc754051(v=ws.11)) will display any groups that exist on the host from which we issued the command, create and delete groups, and add or remove users from groups. It will also display domain group information if the host is joined to the domain. Keep in mind, `net group` must be run against a domain server such as the DC, while `net localgroup` can be run against any host to show us the groups it contains.

#### Net Share

One way of doing so involves using the `net share` command. [Net Share](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh750728(v=ws.11)) allows us to display info about shared resources on the host and to create new shared resources as well.
#### Net View

If we are not explicitly looking for shares and wish to search the environment broadly, we have an alternate command that can be extremely useful, also known as `net view`.

[Net View](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh875576(v=ws.11)) will display to us any shared resources the host you are issuing the command against knows of. This includes domain resources, shares, printers, and more.