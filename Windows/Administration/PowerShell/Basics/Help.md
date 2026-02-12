Get-Help \<command\> \<-online\>
Update-Help -> update help files
Get-Location == cd
Get-ChildItem == dir
Set-Location dir == cd dir
Get-Content file.txt == type file.txt

Get-Command -> list all cmdlets
Get-Command -verb get -> list all cmdlets that has "get" verb
Get-Command -noun windows* -> same thing

Get-Module -> show loaded modules
	-ListAvailable -> shows installed but not loaded


Get-History
	By default, `Get-History` will only show the commands that have been run during this active session. Notice how the commands are numbered; we can recall those commands by using the alias `r` followed by the number to run that command again. For example, if we wanted to rerun the `arp -a` command, we could issue `r 14`, and PowerShell will action it. Keep in mind that if we close the shell window, or in the instance of a remote shell through command and control, once we kill that session or process that we are running, our PowerShell history will disappear. With `PSReadLine`, however, that is not the case. `PSReadLine` stores everything in a file called `$($host.Name)_history.txt` located at `$env:APPDATA\Microsoft\Windows\PowerShell\PSReadLine`.
r \[number\] -> run the command again from history 
```powershell-session
C:\Users\DLarusso\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt   --->>> all history of powershell
```

Clear-Host == cls
Get-Alias
Set-Alias -> `Set-Alias -Name gh -Value Get-Help`



### Hotkeys

|**HotKey**|**Description**|
|---|---|
|`CTRL+R`|It makes for a searchable history. We can start typing after, and it will show us results that match previous commands.|
|`CTRL+L`|Quick screen clear.|
|`CTRL+ALT+Shift+?`|This will print the entire list of keyboard shortcuts PowerShell will recognize.|
|`Escape`|When typing into the CLI, if you wish to clear the entire line, instead of holding backspace, you can just hit `escape`, which will erase the line.|
|`↑`|Scroll up through our previous history.|
|`↓`|Scroll down through our previous history.|
|`F7`|Brings up a TUI with a scrollable interactive history from our session.|


## Some Useful Modules
```powershell-session
Get-Command -Module PowerShellGet 
```
PowerShellGet

```powershell-session
Find-Module -Name AdminToolbox | Install-module
```
AdminToolBox

### Tools To Be Aware Of

Below we will quickly list a few PowerShell modules and projects we, as penetration testers and sysadmins, should be aware of. Each of these tools brings a new capability to use within PowerShell. Of course, there are plenty more than just our list; these are just several we find ourselves returning to on every engagement.

- [AdminToolbox](https://www.powershellgallery.com/packages/AdminToolbox/11.0.8): AdminToolbox is a collection of helpful modules that allow system administrators to perform any number of actions dealing with things like Active Directory, Exchange, Network management, file and storage issues, and more.
    
- [ActiveDirectory](https://learn.microsoft.com/en-us/powershell/module/activedirectory/?view=windowsserver2022-ps): This module is a collection of local and remote administration tools for all things Active Directory. We can manage users, groups, permissions, and much more with it.
    
- [Empire / Situational Awareness](https://github.com/BC-SECURITY/Empire/tree/master/empire/server/data/module_source/situational_awareness): Is a collection of PowerShell modules and scripts that can provide us with situational awareness on a host and the domain they are apart of. This project is being maintained by [BC Security](https://github.com/BC-SECURITY) as a part of their Empire Framework.
    
- [Inveigh](https://github.com/Kevin-Robertson/Inveigh): Inveigh is a tool built to perform network spoofing and Man-in-the-middle attacks.
    
- [BloodHound / SharpHound](https://github.com/BloodHoundAD/BloodHound/tree/master/Collectors): Bloodhound/Sharphound allows us to visually map out an Active Directory Environment using graphical analysis tools and data collectors written in C# and PowerShell.