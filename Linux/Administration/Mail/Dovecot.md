## Dovecot: Mail Delivery Agent (MDA) & IMAP/POP3 Server

**What it is:** Dovecot is a free and open-source **MDA (Mail Delivery Agent)** and a highly popular **IMAP/POP3 server**. Its primary role is to allow users to **access and manage their email mailboxes** which have been delivered by an MTA like Postfix. It integrates seamlessly with Postfix.

**Why it's needed:** Postfix (the MTA) handles receiving emails and putting them into a user's mailbox on the server. Dovecot then provides the interface for email clients (like Thunderbird, Outlook, webmail) to _read_ those emails from the server using IMAP or POP3 protocols. Without Dovecot, users couldn't fetch their mail from a central server.

---

### Installation
`sudo apt install dovecot-imapd dovecot-pop3d`
- `dovecot-imapd`: Enables IMAP functionality.
- `dovecot-pop3d`: Enables POP3 functionality (often less used now, but included for completeness).
- The installation process will typically start the Dovecot service automatically.
### Basic Config
Dovecot's configuration is modular, using multiple files in `/etc/dovecot/conf.d/`.

#### 1. Configure Mail Location (`10-mail.conf`):
- This is the most critical step: telling Dovecot _where_ user mailboxes are stored. It **must match** how Postfix is configured to deliver mail.
- Edit `/etc/dovecot/conf.d/10-mail.conf`:
    ```
    sudo nano /etc/dovecot/conf.d/10-mail.conf
    ```
- Find the `mail_location` line and uncomment/change it to:
    ```
    mail_location = maildir:~/Maildir
    ```
    
    - **`maildir:~/Maildir`**: This is the recommended modern format. It means mail will be stored in a `Maildir` directory within each user's home directory (e.g., `/home/username/Maildir/`). 
	    
    - This must match ::`home_mailbox = Maildir/`:: in Postfix's `main.cf`.
        
    - (Alternatively, if Postfix delivers to `/var/mail` in mbox format: `mail_location = mbox:~/mail:INBOX=/var/mail/%u`)
#### 2. Enable Plaintext Authentication (for testing/internal networks - `10-auth.conf`):

- By default, Dovecot might disable plaintext password transmission for security. For initial testing with Thunderbird (especially without SSL/TLS configured yet), you might need to enable it.
    
- Edit `/etc/dovecot/conf.d/10-auth.conf`:
    ```
    sudo nano /etc/dovecot/conf.d/10-auth.conf
    ```

- Find `disable_plaintext_auth` and set it to `no`:
    ```
    disable_plaintext_auth = no
    ```
    
	- **Security Note:** For production or external access, you should always enforce SSL/TLS (see next point) and disable plaintext auth again to prevent password sniffing.

#### 3. Enable SSL/TLS (Strongly Recommended - `10-ssl.conf`):

- Encrypts communication between the client and Dovecot.
- Edit `/etc/dovecot/conf.d/10-ssl.conf`:
    
    ```
    sudo nano /etc/dovecot/conf.d/10-ssl.conf
    ```
    
- Ensure `ssl = yes`.
- Specify your SSL certificate and key paths (you'll generate these or obtain from a CA):
    
    ```
    ssl_cert = </etc/dovecot/dovecot.pem
    ssl_key = </etc/dovecot/private/dovecot.pem
    ```
    
    - For testing, Dovecot generates self-signed certs by default. For production, use Let's Encrypt or a commercial CA.

#### 4. Restart Dovecot & Manage Firewalls
```
sudo systemctl restart dovecot

sudo ufw allow 143/tcp
sudo ufw allow 993/tcp
sudo ufw enable # if not already enabled
```

#### 5. Security Settings
##### 1. `unix_listener auth-userdb`

- **Location:** Often found in `/etc/dovecot/conf.d/10-master.conf`
- **What it does:** This line defines a **Unix domain socket** (a special file used for inter-process communication on a single system) named `auth-userdb`.
- **Purpose:** It creates a dedicated channel that **other programs (like Postfix)** can use to ask Dovecot to authenticate a user.
    - When a user tries to send email via Postfix using their email client, Postfix can send the username and password to this `auth-userdb` socket.
    - Dovecot then checks the credentials against its user database (e.g., system users, LDAP).
    - Dovecot tells Postfix if the authentication succeeded or failed.
- **Why you need it:** It enables **SASL authentication for Postfix through Dovecot**, allowing your email clients to authenticate against your central user accounts for sending mail. You generally **do need to ensure this is correctly configured and uncommented** if you want Postfix to use Dovecot for authentication.

##### 2. `auth_mechanisms = plain login`

- **Location:** Often found in `/etc/dovecot/conf.d/10-auth.conf`
- **What it does:** This setting specifies which **authentication methods (mechanisms)** Dovecot will accept from email clients.
- **`plain`:** A simple mechanism where the username and password are sent in plaintext (unencrypted) over the connection.
- **`login`:** Another simple mechanism similar to `plain`, also sending credentials largely in plaintext.
- **Why you need it (and cautions):**
    - **Need:** Many older email clients, or clients connecting without SSL/TLS, might only support `plain` or `login`. Enabling them ensures broader compatibility.
    - **Cautions:** Because `plain` and `login` send passwords unencrypted, they are **highly insecure if not used over an SSL/TLS (encrypted) connection.**
    - **Recommendation:** If you have SSL/TLS properly configured for IMAP/POP3 (ports 993/995) and SMTP (port 587 with STARTTLS), then using `plain login` is generally acceptable as the entire connection is encrypted. If not using SSL/TLS, these are a security risk. Dovecot supports stronger mechanisms like `CRAM-MD5` or `DIGEST-MD5` if needed.
---

### Common Integration with Postfix:
Dovecot is often integrated with Postfix to provide **SASL (Simple Authentication and Security Layer) authentication** for outgoing mail. This allows users to authenticate to Postfix via Dovecot's user database, so Postfix knows who is sending mail, especially if they are outside your `mynetworks`. This involves configuring `smtpd_sasl_type = dovecot` and `smtpd_sasl_path = private/auth` in Postfix's `main.cf` and ensuring Dovecot listens on that authentication socket.