# Cloudflare Side
- Moved my domain to Cloudflare, proxying all records
- Created a Zero Trust - Free account

- Created a Cloudflare tunnel pi-ssh under Networks > Connectors
- Created the domain of ssh.nexonet.space under pi-ssh > Published application routes
> I was using Docker for cloudflared instance, but since I left the Docker network in default, localhost wasn't working here. So I changed the URL in application routes to the local IP of Raspberry Pi briefly. But then, I decided to change the network of the Docker container to 'host'

- Created a compose file for container, specifying network_mode as host


# Windows Side
- Created an SSH key
- Enabled the OpenSSH Agent for Windows
- Added my key to the agent to not enter my passphrase every time. Instead, it keeps the unencrypted version in RAM
	- `ssh-add c:/Users/YOU/.ssh/id_ed25519`
- Installed cloudflared via winget
	- `winget install --id Cloudflare.cloudflared`
	- C:\Program Files (x86)\cloudflared
- Manually tried if it is working
	- `ssh -o "ProxyCommand=C:/Program Files (x86)/cloudflared/cloudflared.exe access ssh --hostname %h" atakan@ssh.nexonet.space`
- After confirming it is working, did some settings in MobaXTerm:
	- Session Settings > Network Settings > Proxy Settings
		- Proxy type: local
		- local proxy command: `"C:\Program Files (x86)\cloudflared\cloudflared.exe" access ssh --hostname %host`
		- Port: default (1080)
	- Session Settings > Advanced SSH Settings
		- SSH-Browser type: SCP (SFTP is too slow with cloudflared)
		- **UNCHECK** user private key (it should use windows' SSH agent, checking this makes you ask passphrase every time)
	- Global settings > SSH
		- Check use Windows SSH Key
		- Uncheck Use internal ssh agent "MobAgent"
