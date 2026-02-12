The [wevtutil](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/wevtutil) command line utility can be used to retrieve information about event logs. It can also be used to export, archive, and clear logs, among other commands.

`wevtutil /?`
- el -> enumerate
- gl {"Windows PowerShell"} -> display config info of a specific log, like if logging enabled, max size, perms, location etc.
- gli {"log"}-> status info of log like creation time, last access, write time, file size, number of log records...
  
#### Querying Events
There are many ways we can query for events. For example, let's say we want to display the last 5 most recent events from the Security log in text format. Local admin access is needed for this command.

```cmd-session
C:\htb> wevtutil qe Security /c:5 /rd:true /f:text
```
  
#### Exporting Events

```cmd-session
C:\htb> wevtutil epl System C:\system_export.evtx
```

  
## PowerShell - Listing All Logs

```powershell-session
PS C:\htb> Get-WinEvent -ListLog *
Get-WinEvent -ListLog Security

Get-WinEvent -LogName 'Security' -MaxEvents 5 | Select-Object -ExpandProperty Message  (get the last 5 events, if we want oldest 5, -Oldest)
```


#### Filtering for Logon Failures

We can dig deeper and look at specific event IDs in specific logs. Let's say we only want to look at logon failures in the Security log, checking for Event ID [4625: An account failed to log on](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625). From here, we could use the `-ExpandProperty` parameter to dig deeper into specific events, list logs from oldest to newest, etc.

```powershell-session
PS C:\htb> Get-WinEvent -FilterHashTable @{LogName='Security';ID='4625 '}
```



We can also look at only events with a specific information level. Let's check all System logs for only `critical` events with information level `1`. Here we see just one log entry where the system did not reboot cleanly.
```powershell-session
Get-WinEvent -FilterHashTable @{LogName='System';Level='1'} | select-object -ExpandProperty Message
```