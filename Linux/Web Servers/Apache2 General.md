# 🟢 1. Installation

`sudo apt install apache2 -y   # Debian-based`

> On Red Hat-based systems (RHEL/CentOS/Fedora), the service is called `httpd`.

---

# 🗂️ 2. Key Apache File Structure

| File/Directory                 | Description                                               |
| ------------------------------ | --------------------------------------------------------- |
| `/usr/sbin/httpd`              | Server binary                                             |
| `/etc/httpd`                   | Main config directory (RHEL-based)                        |
| `/etc/httpd/conf`              | Main configuration files                                  |
| `/etc/httpd/conf.d`            | Drop-in configs for modules or virtual hosts              |
| `/etc/apache2/apache2.conf`    | Main config file (Debian-based)                           |
| `/etc/httpd/logs`              | Symlink to `/var/log/httpd`                               |
| `/etc/httpd/modules`           | Symlink to `/usr/lib/httpd/modules`                       |
| `/usr/lib/httpd/modules`       | Directory containing server modules                       |
| `/etc/httpd/run`               | Symlink to `/var/run`                                     |
| `/var/log/httpd`               | Log files                                                 |
| `/var/run/httpd.pid`           | Server PID file                                           |
| `/var/www/html`                | Default document root                                     |
| `/etc/apache2/sites-enabled`   | Enabled site configs (Debian)                             |
| `/etc/apache2/sites-available` | Available site configs (Debian; use `a2ensite` to enable) |
| `/etc/httpd/conf.d`<br>        | Enabled site configs (RHEL)                               |

---

# ⚙️ 3. Main Config File

#### Debian: `/etc/apache2/apache2.conf`

#### RHEL: `/etc/httpd/conf/httpd.conf`

### Common Directives:

- **ServerRoot**: Top of config/log directory tree (e.g., `/etc/httpd`)
    
- **ServerName**: Domain name and port Apache identifies as
    
- **DocumentRoot**: Web root directory (default: `/var/www/html`)
    
- **ErrorLog**: Default: `logs/error_log` → usually `/var/log/httpd/error_log`
    
- **Listen**: Port Apache listens on (e.g., `Listen 80`)


> The main config can include `Include` or `IncludeOptional` directives to load other config files (like in `conf.d/` or `sites-enabled/`).

[[Apache2 Config]]




---

# 🧾 4. Directory Permissions Example



```
<Directory /var/www/html>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```

📁 **Defined in**:

- Main config or drop-in files (e.g., `/etc/httpd/conf.d/denem.conf`)
    

---

# 🌐 5. Hosting Multiple Sites (Virtual Hosts)

Use **VirtualHost** blocks:

```
<VirtualHost *:80>
    ServerName nexonet.space
    DocumentRoot /var/www/nexonet.space

    <Directory /var/www/nexonet.space>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

📁 **Where to place:**

- **Debian**: `/etc/apache2/sites-available/nexonet.space.conf`
    
    - Enable it: `sudo a2ensite nexonet.space.conf && sudo systemctl reload apache2`
        
- **RHEL**: `/etc/httpd/conf.d/nexonet.space.conf`
    

📝 After creating, **reload Apache**:

```
sudo systemctl reload apache2   # Debian
sudo systemctl reload httpd     # RHEL
```

---

# 🛠️ 6. Extra Notes

- `apachectl` is a common wrapper to manage Apache (especially on RHEL).
    
- `a2ensite` / `a2dissite` (Debian) are used to enable/disable site configs.
    
- You can serve files to other machines (for exploitation, CTFs, etc.) by placing them under `/var/www/html` and accessing via `wget`, `curl`, browser, etc.
    

---

# 🔐 7. .htaccess and Modules

### `.htaccess`

- Enables per-directory config without editing main Apache files.
    
- Must be allowed via: `AllowOverride All`
    

### Common Useful Modules:

|Module|Purpose|
|---|---|
|`mod_rewrite`|URL rewriting|
|`mod_ssl`|HTTPS|
|`mod_security`|WAF (Web Application Firewall)|

Enable with:

```
sudo a2enmod rewrite ssl security2   # Debian
sudo systemctl reload apache2
```


# 8. Rewrite Engine
It is used in .htaccess files and in conf.d/ files. It can force using HTTPS over HTTP.
```
RewriteEngine On 
RewriteCond %{HTTPS} off 
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

This can cause some problems if hosting more than 1 website. 

If you have only 1 website, that is the default config the apache will use. You can create a 00-default.conf to overwrite it.

So if you create a second website with only HTTP, it automatically will redirect to the old website with HTTPS enabled.

**Note to self: Research this more**