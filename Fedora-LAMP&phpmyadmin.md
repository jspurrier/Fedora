# Fedora 29 LAMP

`sudo dnf install httpd`

enable and start apache
`sudo systemctl enable httpd`
`sudo systemctl start httpd`

Firewall
`sudo firewall-cmd --add-service={http,https} --permanent`
`sudo firewall-cmd --reload`

next PHP
`sudo dnf install php php-common`

next PHP extra libs

`sudo dnf install php-pecl-apcu php-cli php-pear php-pdo php-mysqlnd php-pgsql php-pecl-mongodb php-pecl-memcache php-pecl-memcached php-gd php-mbstring php-mcrypt php-xml php-cli php-php-gettext php-mbstring php-mcrypt php-mysqlnd php-pear php-curl php-gd php-xml php-bcmath php-zip`


restart apache
`sudo systemctl restart httpd`

Next Mariadb or mysql 
`sudo dnf install mariadb-server`

Next start and enable mysql/mariadb
`sudo systemctl enable mariadb`
`sudo systemctl start mariadb`

Next run final install setup for mariadb/mysql
`sudo mysql_secure_installation`

Finally add phpmyadmin
`sudo dnf install phpMyAdmin`

Enable access for your IP or for all(all is dangerous as entire internet)
`nano /etc/httpd/conf.d/phpMyAdmin.conf`

```
Change this line below:
Require ip <insert IP or require all IP
```

Restart apache
`sudo systemctl restart httpd`
