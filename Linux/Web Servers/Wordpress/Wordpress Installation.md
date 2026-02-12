https://docs.fedoraproject.org/en-US/fedora-server/tutorials/wordpress-installation/

_For the sake of completeness_: Even though Wordpress is widely used, you should carefully consider whether you really need a dynamic CMS that generates every page with every request anew.

- If your pages remain largely unchanged once they have been created, various static site generators are probably more practical and less time-consuming to maintain.
    
- Be prepared for the fact that the ongoing operation of Wordpress requires considerable effort. Wordpress is known for recurring security issues and requires ongoing attention and maintenance.
    
    At minimum, Wordpress should be installed in a container. Fedora Server offers several options for this, including some with little additional management effort.


## Prerequisites

- We assume a correctly installed Fedora Server Edition release 38 or 39. For details see [Fedora Server Installation Guide](https://docs.fedoraproject.org/en-US/fedora-server/installation/).
    
- Wordpress stores most of the content in a database. Accordingly, it requires access to a working database system and doesn’t even startup without. Currently, it [no longer enables to use PostgreSQL](https://wordpress.org/plugins/postgresql-for-wordpress/), the Fedora Server Edition preferred and specifically supported database system. It just supports MariaDB or MySQL, which are included in Fedora as well.
    
    So you have to install either MariaDB or MySQL following [Installing MySQL/MariaDB](https://docs.fedoraproject.org/en-US/fedora-server/tutorials/wordpress-installation/#:quickdocs/installing-mysql-mariadb.adoc). In terms of Wordpress, both systems work equally smoothly. Following Fedoras preferrence for truely OSS software we use MariaDB here.
    
    Before you start installation, create the [required storage](https://docs.fedoraproject.org/en-US/fedora-server/installation/#_storage_organization). The easiest and quickest way is to use Cockpit (select the storage tab and then the appropriate Volume Group in the upper right corner).
    
- Furthermore, Wordpress needs a web server to deliver the pages. Fedora Server Edition and the Fedora WordPress package support _httpd_, the Fedora version of the Apache Web server. Of course, other Web servers are also possible here. You will then have to do the adaptation to Wordpress yourself.
    
    If not already done install the [Fedora Web Server package](https://docs.fedoraproject.org/en-US/fedora-server/services/httpd-basic-setup/). If your server will just server the Wordpress site, you may omit the section "Setup a Web site".


```bash
dnf install  wordpress


MariaDB [(none)]> show databases;
MariaDB [(none)]> CREATE DATABASE wordpress ;
MariaDB [(none)]> CREATE USER 'wordpress'   IDENTIFIED BY 'wp-test-proj';
MariaDB [(none)]> GRANT ALL PRIVILEGES ON wordpress.*  TO 'wordpress';
MariaDB [(none)]> quit;



[…]# vim /etc/wordpress/wp-config.php
define( 'DB_NAME', 'xxxxx' );
define( 'DB_USER', 'xxxx' );
define( 'DB_PASSWORD', 'xxxxxxxx' );
define( 'DB_HOST', 'xxxx' );




[…]# vim /etc/httpd/conf.d/wordpress.conf

Alias /wordpress /usr/share/wordpress

# Access is only allowed via local access
# Change this once configured

<Directory /usr/share/wordpress>
  AllowOverride Options
  #Require local                       # <== mod
  Require all granted                  # <== add
</Directory>

```

