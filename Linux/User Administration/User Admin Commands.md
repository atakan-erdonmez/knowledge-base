
There are four main user administration files:

1. /etc/passwd: User accounts
2. /etc/shadow: User password
	- !! means password does not exist   
3. /etc/group: Group information
4. /etc/gshadow: Group passwords

- useradd: -d→different home directory, -u→user id, -g→group id, -G→ multi group (secondary), -M→no home folder, -e→expiry, -c→comment, -s→custom shell, -f→password expire,       -m-> create home directory

- usermod: -c→comment, -d→modify home directory, -e→expiry, -g→primary group, -a→add to secondary group, -G→secondary group, -l→login name (username), -L→lock the account, -U ->unlock account, -d→default home dir, -s->change shell


- userdel
- groupadd: -f→force, -g→gid, -r→system group
- groupmod: -g→new gid, -n→new name
- groupdel
- gpasswd: -a→add user, -d→delete user, -r→remove password & change password of a group (gpasswd groupname)
- newgrp: Log in to a new group, change the gid

