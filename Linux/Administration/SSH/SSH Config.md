SSH config settings (/etc/ssh/sshd_config

1. PermitRootLogin no
2. AllowUsers atakan bora
    1. AllowGroups adminler gururlular
3. DenyUsers murat elif
    1. DenyGroups enazindan
4. Port degistir buyuk ve random bir sayi yap
5. LoginGraceTime 1m → sifre girmeyince iptal olma suresi / timeout
6. ListenAddress 192.168.2.100 ⇒ Birden fazla IP’si olan server’larda sadece belli IP’lere baglanmaya izin ver
7. ClientAliveInterval 600 → 10 dakika sonra timeout
    1. ClientAliveCountMax 0 ⇒ Check for client is active

xinetd bir servis grubudur. Genelde de deprecated programlar bulunur (rlogin, rsh, rsync, svn, talk, telnet vs.) /etc/xinetd.d dizinini kullanir.


> ssh-keygen -R raspberrypi : remove keys for that known host


PermitRootLogin prohibit-password -> root only can login with key

## SSH Keys

There are 2 types of keys, host and user.

### Host Keys
They are in /etc/ssh/ssh_host_\*. These belong to the machine, they shouldn't be deleted unless converting into a template [[CT Template]] [[VM Template & Cloud-init]]

You can re-create them with `ssh-keygen -A`


# SSH Config File

~/.ssh/config

```
Host dev
    HostName dev.example.com
    User john
    Port 2322
    IdentityFile # specific key 
```

ssh dev -> these parameters

https://linuxize.com/post/using-the-ssh-config-file/

# SSH Agent
Agents can be used to keep the decrypted private key in memory, so you don't have to put the passphrase

```
eval "$(ssh-agent -s)" # start service
ssh-add ~/.ssh/id_ed25519 # add the key
ssh-add -l # List keys loaded in agent
ssh-add -d ~/.ssh/id_ed25519 # remote key from agent
ssh-add -D # remove all keys from agent
```