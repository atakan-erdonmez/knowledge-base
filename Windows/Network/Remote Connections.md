## SSH

```powershell-session
 Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'

Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0(whichever version you want)
```
Add SSH server/client functionality

##### Service Sshd
```powershell-session
Start-Service sshd
Set-Service -Name sshd -StartupType 'Automatic' 
```


## WinRM

[Windows Remote Management (WinRM)](https://docs.microsoft.com/en-us/windows/win32/winrm/portal) can be configured using dedicated PowerShell cmdlets and we can enter into a PowerShell interactive session as well as issue commands on remote Windows target(s). We will notice that WinRM is more commonly enabled on Windows Server operating systems, so IT admins can perform tasks on one or multiple hosts. It's enabled by default in Windows Server.

Because of the increasing demand for the ability to remotely manage and automate tasks on Windows systems, we will likely see WinRM enabled on more & more Windows desktop operating systems (Windows 10 & Windows 11) as well. When WinRM is enabled on a Windows target, it listens on logical ports `5985` & `5986`.



```powershell-session
winrm quickconfig -> enable & config
```
As can be seen in the above output, running this command will automatically ensure all the necessary configurations are in place to:

- Enable the WinRM service
- Allow WinRM through the Windows Defender Firewall (Inbound and Outbound)
- Grant administrative rights remotely to local users


 IT admins should take further steps to harden these WinRM configurations, especially if the system will be remotely accessible over the Internet. Among some of these hardening options are:

- Configure TrustedHosts to include just IP addresses/hostnames that will be used for remote management
- Configure HTTPS for transport
- Join Windows systems to an Active Directory Domain Environment and Enforce Kerberos Authentication


**Check if WinRM is enabled**
```powershell-session
Test-WSMan -ComputerName "10.129.224.248" -> unauthorized

Test-WSMan -ComputerName "10.129.224.248" -Authentication Negotiate -> authorized
```


**Connection**
```powershell-session
Enter-PSSession -ComputerName 10.129.224.248 -Credential htb-student -Authentication Negotiate
```


**NOTE**: We can perform this same action from a Linux-based attack host with PowerShell core installed (like in Pwnbox). Remember that PowerShell is not exclusive to Windows and will run on other operating systems now.