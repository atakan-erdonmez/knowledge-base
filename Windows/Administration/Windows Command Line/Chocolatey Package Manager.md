#### Chocolatey Package Manager
Installation:

`PS C:\\htb> Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('<https://chocolatey.org/install.ps1>'))` 

```jsx
choco upgrade chocolatey -y

choco info vscode

choco install python vscode
##### Exclusions
 To make sure Defender does not mess up our plans, we will add some exclusion rules to ensure our tools stay in place.
- `C:\Users\your user here\AppData\Local\Temp\chocolatey\`  
- `C:\Users\your user here\Documents\git-repos\`
- `C:\Users\your user here\Documents\scripts\`

```powershell-session
PS C:\htb> Add-MpPreference -ExclusionPath "C:\Users\your user here\AppData\Local\Temp\chocolatey\"
```

==Before executing any scripts, we need to change the execution policy==


```powershell
# Choco build script

write-host "*** Initial app install for core tools and packages. ***"

write-host "*** Configuring chocolatey ***"
choco feature enable -n allowGlobalConfirmation

write-host "*** Beginning install, go grab a coffee. ***"
choco upgrade wsl2 python git vscode openssh openvpn netcat nmap wireshark burp-suite-free-edition heidisql sysinternals putty golang neo4j-community openjdk

write-host "*** Build complete, restoring GlobalConfirmation policy. ***"
choco feature disable -n allowGlobalCOnfirmation
```

When scripting with Chocolatey, the developers recommend a few rules to follow:

- always use `choco` or `choco.exe` as the command in your scripts. `cup` or `cinst` tends to misbehave when used in a script.
    
- when utilizing options like `-n` it is recommended that we use the extended option like `--name`.
    
- Do not use `--force` in scripts. It overrides Chocolatey's behavio