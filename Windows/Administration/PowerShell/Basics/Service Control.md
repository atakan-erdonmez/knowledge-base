[[Services General]]

get-service | Select-Object -Property DisplayName,Name,Status | Sort-Object DisplayName | fl  -> show services in a clear way

```powershell-session
Get-Help *-Service  

Get-Service | ft DisplayName,Status
Get-Service | where DisplayName -like '*Defender*' | ft DisplayName,ServiceName,Status
Get-Service WinDefend
```


```powershell-session
Start-Service WinDefend
Stop-Service Spooler

get-service spooler | Select-Object -Property Name, StartType, Status, DisplayName 
```

```
Set-Service -Name Spooler -StartType Disabled
```

## How Do We Interact with Remote Services using PowerShell?

Now that we know how to work with services, let us look at how we can interact with remote hosts. Since Mr. Tanaka's host is in a domain, we can easily query and check the running services on other hosts. The `-ComputerName` parameter allows us to specify that we want to query a remote host.

```powershell-session
get-service -ComputerName ACADEMY-ICL-DC
Get-Service -ComputerName ACADEMY-ICL-DC | Where-Object {$_.Status -eq "Running"}

invoke-command -ComputerName ACADEMY-ICL-DC,LOCALHOST -ScriptBlock {Get-Service -Name 'windefend'}

```

Let us break this down now:

- `Invoke-Command`: We are telling PowerShell that we want to run a command on a local or remote computer.
- `Computername`: We provide a comma-defined list of computer names to query.
- `ScriptBlock {commands to run}`: This portion is the enclosed command we want to run on the computer. For it to run, we need it to be enclosed in {}.