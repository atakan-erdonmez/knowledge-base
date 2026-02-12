From the CLI, we have several options to access the Registry and manage our keys. The first is using [reg.exe](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/reg). `Reg` is a dos executable explicitly made for use in managing Registry settings. The second is using the `Get-Item` and `Get-ItemProperty` cmdlets to read keys and values. If we wish to make a change, the use of New-ItemProperty will do the trick.

```powershell-session
Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run | Select-Object -ExpandProperty Property

Get-ChildItem -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Recurse

Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
```

#### Reg.exe
```powershell-session
PS C:\htb> reg query HKEY_LOCAL_MACHINE\SOFTWARE\7-Zip

HKEY_LOCAL_MACHINE\SOFTWARE\7-Zip
    Path64    REG_SZ    C:\Program Files\7-Zip\
    Path    REG_SZ    C:\Program Files\7-Zip\
```

## Finding Info In The Registry

For us as pentesters and administrators, finding data within the Registry is a must-have skill. This is where `Reg.exe` really shines for us. We can use it to search for keywords and strings like `Password` and `Username` through key and value names or the data contained. Before we put it to use, let's break down the use of `Reg Query`. We will look at the command string `REG QUERY HKCU /F "password" /t REG_SZ /S /K`.

- `Reg query`: We are calling on Reg.exe and specifying that we want to query data.
- `HKCU`: This portion is setting the path to search. In this instance, we are looking in all of HKey_Current_User.
- `/f "password"`: /f sets the pattern we are searching for. In this instance, we are looking for "Password".
- `/t REG_SZ`: /t is setting the value type to search. If we do not specify, reg query will search through every type.
- `/s`: /s says to search through all subkeys and values recursively.
- `/k`: /k narrows it down to only searching through Key names.
  
### New Registry Key

```powershell-session
PS C:\htb> New-Item -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\ -Name TestKey


New-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\TestKey -Name  "access" -PropertyType String -Value "C:\Users\htb-student\Downloads\payload.exe"
```

With Reg.exe:
```powershell
reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce\TestKey" /v access /t REG_SZ /d "C:\Users\htb-student\Downloads\payload.exe"  
```

### Remove Key
```powershell-session
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\TestKey -Name  "access"
```