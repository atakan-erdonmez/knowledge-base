#### Permissions
```powershell
PS C:\\htb> Get-ExecutionPolicy -List

Scope ExecutionPolicy
----- ---------------
MachinePolicy Undefined
UserPolicy Undefined
Process Undefined
CurrentUser Undefined
LocalMachine Undefined

PS C:\\htb> Set-ExecutionPolicy Unrestricted -Scope Process

Setup the exec policy for scope as specified on top
```

```powershell
PS C:\\htb> Import-Module PSWindowsUpdate (download and import updates)

PS C:\\htb> Install-WindowsUpdate -AcceptAll (install them)

PS C:\\htb> Restart-Computer -Force
```

```