It is a driver to manage UPS and other power equipment. Since distros might not have the latest drivers, it is best to compile from the source 
[[Tuncmatik UPS Installation]]

# File Hierarchy
These are all under `/etc/nut`

### nut.conf
The master switch for the whole NUT suite. It determines mode like standalone, netclient etc.

### ups.conf
This is the actual driver config. It specifies which subdriver and protocol to be used to understand the signal coming from the USB.

### upsd.conf
Controls who can listen to the UPS data. It includes `LISTEN 127.0.0.1` line so the server only talks with localhost.

### upsd.users
The username and password file for the server. Even though everything is in the same machine, **upsmon** needs permission to ask the **upsd** for data.

### upsmon.conf
It is the file that triggers actions like halt or shutdown. It has the `MONITOR tuncmatik@localhost 1 upsmon changeme master`. 1 is the power value



### The Flow of Information

1. **`nutdrv_qx`** polls the USB port $\rightarrow$ "Hey UPS, you okay?"
2. **The UPS** says $\rightarrow$ "I'm on battery!"
3. **`upsd`** (The Server) reads that status from the driver    
4. **`upsmon`** (The Monitor) asks `upsd` $\rightarrow$ "Is the power okay?"
5. **`upsd`** replies $\rightarrow$ "No, we are on battery."
6. **`upsmon`** waits until the battery hits "Critical," then runs your shutdown script.

# Management


| Command                                                           | Purpose                                                                             |
| ----------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `upsc tuncmatik`                                                  | See everything                                                                      |
| `upsc tuncmatik ups.status`                                       | Check specific variable                                                             |
| `upsc tuncmatik \| grep -E "status\|charge\|runtime\|load"`       | Useful info                                                                         |
| `upscmd -l tuncmatik`                                             | List what UPS can actually do, list commands                                        |
| `upscmd -u upsmon -p PASSWORD tuncmatik beeper.toggle`            | Silence the beep                                                                    |
| `upscmd -u upsmon -p changeme tuncmatik test.battery.start.quick` | Start a quick battery test                                                          |
| `upsrv tuncmatik`                                                 | If UPS allows internal logic (like what % battery is low), show what can be changed |
| `upsrw -s battery.charge.low=20 -u upsmon -p changeme tuncmatik`  | Change low battery threshold                                                        |
| `sudo upsmon -c fsd`                                              | Simulate a critical shutdown. fsd stands for 'forced shutdown'                      |
