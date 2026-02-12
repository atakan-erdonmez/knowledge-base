These can be set in main config file, or page-specific file. They are in <\Directory> unless specified otherwise.
Show httpd config:
```
https -S
```

>  `apachectl configtest` (or `apache2ctl configtest` on some distros) checks the **syntax** of your Apache configuration files without restarting the server.


> All files should be owned by www-data / apache for security purposes


#### Alias
alias /alias_name /folder
# Order (allow, deny) (legacy)
```
<Directory /var/www/html>
	Order deny,allow
	Deny from all
	Allow from IP
</Directory>
```

This enables controlling specific networks, hostnames or IPs to allow or deny to access.
# Indexes
### DirectoryIndex
This sets the index page. Default is index.html
### Indexes
Typing this after Options enables the use of index

> You can either use `Options +Indexes -FollowSymLinks`, or just type or not type to specify enable/disable
#### Example
```
<Directory /var/www/html/file_share>
	Options Indexes
</Directory>
```

# .htaccess & .htpassword
## .htaccess
🔹 What is `.htaccess`?
`.htaccess` (Hypertext Access) is a configuration file used by Apache **per directory** to override global server settings. It allows you to configure access control, redirects, rewrites, and other directives _without modifying_ the main Apache config files.

### 🔧 How to Enable `.htaccess` Use

Apache must allow overrides using the `AllowOverride` directive in the main config (`apache2.conf` or specific virtual host files):
#####  1. Redirects
```
Redirect /old-page.html /new-page.html
```
##### 2. Rewrites (SEO-friendly URLs)
```
RewriteEngine On 
RewriteRule ^about$ about.html [L]
```
##### 3. Custom Error Page
```
ErrorDocument 404 /404.html
```
##### 4. Deny Access by IP
```
Order Deny,Allow 
Deny from 192.168.1.100
```
##### 5. Basic Authentication
```
AuthType Basic
AuthName "Restricted page, please enter password"
AuthUserFile /etc/httpd/conf.d/.htpasswd
Require valid-user
```
> **Needs AllowOverride AuthConfig FileInfo** in site config file
## 🔒 `.htpasswd` – User Authentication File

Used together with `.htaccess` for **Basic HTTP Authentication**.
### **1. Create password file**
```
htpasswd -c /etc/apache2/.htpasswd myuser
```
- Use `-c` only the first time to create the file. Omit `-c` to add more users.

### **2. In `.htaccess`**
```
AuthType Basic
AuthName "Restricted Area"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```
Now, accessing that directory via browser will prompt for username and password.

---

##### 🔥 Security Note:
- Place `.htpasswd` **outside** the web root if possible.
- Use `.htaccess` only when per-directory customization is needed. Otherwise, configure inside the main Apache config for performance.

# UserDir
If you enable UserDir, the user can create and share webpages on their home page. [[SELinux#Booleans]] set should be done.

```
# UserDir    disabled
UserDir    folder_name
```