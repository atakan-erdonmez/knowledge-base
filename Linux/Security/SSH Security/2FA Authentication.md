##### Google Authenticator
```shell-session
[cry0l1t3@VPS ~]$ sudo apt install libpam-google-authenticator -y
[cry0l1t3@VPS ~]$ google-authenticator

Do you want authentication tokens to be time-based (y/n) y

Warning: pasting the following URL into your browser exposes the OTP secret to Google:
  https://www.google.com/chart?chs=200x200&chld=M|0&cht=qr&chl=otpauth://totp/cry0l1t3@parrot%3Fsecret%...SNIP...%26issuer%3Dparrot

   [ ---- QR Code ---- ]

Your new secret key is: ***************
Enter code from app (-1 to skip):
```

If we follow these steps, then a `QR code` and a `secret key` will appear in our terminal, which we can then scan with the Google Authenticator app or enter the secret key there. Once we have scanned the QR code or entered the secret key, we will see the first `OTP` (six-digit number) on our smartphone. We enter this in our terminal to synchronize and authorize Google Authenticator on our smartphone and our VPS with Google.

The module will then generate several `emergency scratch codes` (`backup codes`), which we should save safely. These will be used in case we lose our smartphone. Should this happen, we can then log in with the `backup codes`.

##### PAM Configuration
Next, we need to configure the [PAM](https://en.wikipedia.org/wiki/Linux_PAM) module for the SSH daemon. To do this, we first create a backup of the file and open the file with a text editor such as Vim.

###### /etc/pam.d/sshd
```shell-session
#@include common-auth

...SNIP...

auth required pam_google_authenticator.so
auth required pam_permit.so
```

Next, we need to adjust our settings in our SSH daemon to allow this authentication method. In this configuration file (`/etc/ssh/sshd_config`), we need to add two new lines at the end of the file as follows:

/etc/ssh/sshd_config
```shell-session
...SNIP...

AuthenticationMethods publickey,keyboard-interactive
PasswordAuthentication no
```

Then, restart the sshd service.


### SCP Syntax
```shell-session
scp -i <ssh-private-key> -r <directory to transfer> <username>@<IP/FQDN>:<path>
```