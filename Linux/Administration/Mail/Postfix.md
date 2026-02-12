For more details, check [[Mail Server - Gemini.pdf]]
# Config
## `/etc/postfix/main.cf` -> main config
- Normally, `inet_interfaces=localhost` so users on same device can mail each other with:
```
mail -s "Mail Subject" atakan@nexonet.space

[yazinin kendisi]
CTRL^D
```
`/var/log/maillog` -> mail log
### Myhostname
Used for specifying the hostname of the mail server
mail.example.com
### mydomain
Mail domain
example.com
### myorigin
All mail sent from this mail server will look as though it came from this option
$mydomain
### mydestination
Basically whitelist of possible receivers. 
- It has $myhostname, which allows users on the same system to mail each other
- You can add external IP ranges to allow emailing external clients.
- You can add $mydomain to allow any device with your domain to mail each other.

### relayhost
Use that server as a relayhost, a proxy for mail forwarding
### mynetwork
Only accept emails from this specified network
### inet_interfaces
Which interfaces are allowed (??)
Can be all
### inet_protocols
Which protocols to work with

> To show queue:
> `postqueue -p`
> `mailq`
> `viewqueue`

> `postfix q` -> flush the queue and deliver all emails
# Mailx
The `mailx` program (also called **s-nail**, **BSD mail**, or **Heirloom mailx**) is a **command-line email client** used to:

- **Compose and send emails** from the terminal
- **Read local mail** from **`/var/mail/username`**
- **Send mail using SMTP**, often via `sendmail` or `postfix` in the background

### 🧩 What it is **not**:
- It’s **not a mail server**.
- It doesn’t receive mail on its own — that’s Postfix’s job.
### 🧪 Common use:
`echo "Hello" | mail -s "Test Subject" someone@example.com`

This sends a basic email using the system's MTA (Postfix).


