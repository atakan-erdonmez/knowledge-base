| Signal    | Number | Meaning                           | Common Usage                     |
| --------- | ------ | --------------------------------- | -------------------------------- |
| `SIGTERM` | 15     | Graceful termination              | `kill PID` (default)             |
| `SIGKILL` | 9      | Immediate kill (cannot be caught) | `kill -9 PID`                    |
| `SIGINT`  | 2      | Interrupt from keyboard (Ctrl+C)  | Stops foreground process         |
| `SIGTSTP` | 20     | Terminal stop (Ctrl+Z)            | Suspend process                  |
| `SIGHUP`  | 1      | Hangup / restart signal           | Restart daemons                  |
| `SIGCHLD` | 17     | Child stopped/terminated          | Used by parents to reap zombies  |
| `SIGCONT` | 18     | Continue if stopped               | After `SIGSTOP`/`SIGTSTP`        |
| `SIGSTOP` | 19     | Stop (cannot be ignored)          | Like `SIGTSTP` but unconditional |