#### Built-In Accounts

|**Account**|**Description**|
|---|---|
|`Administrator`|This account is used to accomplish administrative tasks on the local host.|
|`Default Account`|The default account is used by the system for running multi-user auth apps like the Xbox utility.|
|`Guest Account`|This account is a limited rights account that allows users without a normal user account to access the host. It is disabled by default and should stay that way.|
|`WDAGUtility Account`|This account is in place for the Defender Application Guard, which can sandbox application sessions.|


PS > Get-LocalGroup -> show all local groups

General PS
	Like most other things in PowerShell, we use the `get`, `new`, and `set` verbs to find, create and modify users and groups. If dealing with local users and groups, `localuser & localgroup` can accomplish this. For domain assets, `aduser & adgroup` does the trick. If we were not sure, we could always use the `Get-Command *user*` cmdlet to see what we have access to.

Get-LocalUser -> show all local users
New-LocalUser - create local user
	New-LocalUser -Name "JLawrence" -NoPassword
Set-localuser
	PS C:\htb> $Password = Read-Host -AsSecureString
	\*\*\*\*\*\*\*
	PS C:\htb> Set-LocalUser -Name "JLawrence" -Password $Password -Description "CEO EagleFang"

Get-LocalGroup

Get-LocalGroupMember -Name "Users" -> Inspect "Users" group
Add-LocalGroupMember -Group "Remote Desktop Users" -Member "JLawrance"

### Managing Domain Users and Groups

Before we can access the cmdlets we need and work with Active Directory, we must install the `ActiveDirectory` PowerShell Module. If you installed the AdminToolbox, the AD module might already be on your host. If not, we can quickly grab the AD modules and get to work. One requirement is to have the optional feature `Remote System Administration Tools` installed. This feature is the only way to get the official ActiveDirectory PowerShell module. The edition in AdminToolbox and other Modules is repackaged, so use caution.

#### Installing RSAT

```powershell-session
PS C:\htb> Get-WindowsCapability -Name RSAT* -Online | Add-WindowsCapability -Online
```
  
Locating The AD Module

```powershell-session
PS C:\htb> Get-Module -Name ActiveDirectory -ListAvailable 
```
  
Locate User  ->  Get-ADUser

```powershell-session
PS C:\htb> Get-ADUser -Filter *
PS C:\htb>  Get-ADUser -Identity TSilver
Get-ADUser -Filter {EmailAddress -like '*greenhorn.corp'}
```


New ADUser

```
PS C:\htb> New-ADUser -Name "MTanaka" -Surname "Tanaka" -GivenName "Mori" -Office "Security" -OtherAttributes @{'title'="Sensei";'mail'="MTanaka@greenhorn.corp"} -Accountpassword (Read-Host -AsSecureString "AccountPassword") -Enabled $true 

AccountPassword: ****************
PS C:\htb> Get-ADUser -Identity MTanaka -Properties * | Format-Table Name,Enabled,GivenName,Surname,Title,Office,Mail

Name    Enabled GivenName Surname Title  Office   Mail
----    ------- --------- ------- -----  ------   ----
MTanaka    True Mori      Tanaka  Sensei Security MTanaka@greenhorn.corp
```

Changing a Users Attributes

```
PS C:\htb> Set-ADUser -Identity MTanaka -Description "Caresizlik ve gucsuzluk icinde olan" 
```


