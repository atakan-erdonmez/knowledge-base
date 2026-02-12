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

`PS C:\\htb> Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('<https://chocolatey.org/install.ps1>'))` → chocolatey package manager download

```jsx
choco upgrade chocolatey -y

choco info vscode

choco install python vscode
```