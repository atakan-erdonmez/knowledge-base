sc -> service controller
	sc query type=service
	sc query windefend
	sc start|stop windefend
	sc config wuauserv start= disabled/auto

Windows update services -> wuauserv, bits

tasklist /svc -> list services with PID
net start -> list active services
net stop|pause|continue

wmic service list brief -> list all services, regarding status