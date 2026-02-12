**Invoke-Webrequest** -> The cmdlet used for many web-related things including GET/POST, download files, access HTML files etc.

Example:

```powershell-session
Invoke-WebRequest -Uri "URL" -Method GET | Get-Member
Invoke-WebRequest -Uri "URL" -Method GET | Get-Member | fl Images -> just images

```

fl RawContent gives us raw HTML file.


###### Downloading:

```powershell-session
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Recon/PowerView.ps1" -OutFile "C:\PowerView.ps1"
```

###### If Invoke-Webrequest is unusable:

```powershell-session
(New-Object Net.WebClient).DownloadFile("https://github.com/BloodHoundAD/BloodHound/releases/download/4.2.0/BloodHound-win32-x64.zip", "Bloodhound.zip")
```