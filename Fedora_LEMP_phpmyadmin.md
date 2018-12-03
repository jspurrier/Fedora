# Fedora 29 LEMP

`sudo dnf install nginx`

enable and start apache
`sudo systemctl enable nginx`
`sudo systemctl start nginx`

Firewall
`sudo firewall-cmd --add-service={http,https} --permanent`
`sudo firewall-cmd --reload`

next PHP
`sudo dnf install php-fpm php-common`

next PHP extra libs

`dnf install php-opcache php-pecl-apcu php-cli php-pear php-pdo php-mysqlnd php-pgsql php-pecl-mongodb php-pecl-redis php-pecl-memcache php-pecl-memcached php-gd php-mbstring php-mcrypt php-xml`

Start PHP
`systemctl enable php-fpm.service`
`systemctl start php-fpm.service`

restart nginx
`sudo systemctl restart nginx`

configure NGINX and PHP-FPM
`cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak`
`cp /etc/nginx/nginx.conf.default /etc/nginx/nginx.conf`

Modify
`nano /etc/php-fpm.d/www.conf`
To
```
;listen = /run/php-fpm/www.sock
listen = 127.0.0.1:9000
```

Create Directory layouts for site with better logs
`mkdir -p /srv/www/testsite.local/public_html`
`mkdir -p /var/log/nginx/testsite.local`
`chown -R apache:apache /srv/www/testsite.local`
`chown -R nginx:nginx /var/log/nginx`

Create Virtual hosts directories in /etc/nginx
`mkdir /etc/nginx/sites-available`
`mkdir /etc/nginx/sites-enabled`

Add following lines to /etc/nginx/nginx.conf file, after “include /etc/nginx/conf.d/*.conf” line (inside http block).
```
 Load virtual host conf files. 
include /etc/nginx/sites-enabled/*;
```
Create Test file in /etc/nginx/sites-available/testsite.local
```
server {
    server_name testsite.local;
    access_log /var/log/nginx/testsite.local/access.log;
    error_log /var/log/nginx/testsite.local/error.log;
    root /srv/www/testsite.local/public_html;

    location / {
        index index.html index.htm index.php;
    }

    location ~ \.php$ {
        include /etc/nginx/fastcgi_params;
        fastcgi_pass  127.0.0.1:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```
Link and reload
`cd /etc/nginx/sites-enabled/`
`ln -s /etc/nginx/sites-available/testsite.local`
`systemctl restart nginx`

403 Error probably SELinux issue.. Commands to correct
`chcon -R -t httpd_sys_content_t /srv/www/testsite.local/public_html`
`chcon -R -t httpd_sys_rw_content_t /srv/www/testsite.local/public_html`

Suggest restarting both nginx and php once more for good measure
`sudo systemctl restart nginx php-fpm`

Next Mariadb or mysql 
`sudo dnf install mariadb-server`

Next start and enable mysql/mariadb
`sudo systemctl enable mariadb`
`sudo systemctl start mariadb`

Next run final install setup for mariadb/mysql
`sudo mysql_secure_installation`

Finally add phpmyadmin
`sudo dnf install phpMyAdmin`

link phpmyadmin to your html that you want active for
`sudo ln -s /usr/share/phpMyAdmin /usr/share/nginx/html`
`sudo sudo ln -s /usr/share/phpMyAdmin /srv/www/testsite.local/public_html`

Enable access for your IP or for all(all is dangerous as entire internet) (may or may not be needed)
`nano /etc/httpd/conf.d/phpMyAdmin.conf`

```
Change this line below:
Require ip <insert IP or require all IP
```
Selinux might throw fits disable if you run into troubles 
`setenforce 0`


Restart nginx and php one last time
`sudo systemctl restart nginx php-fpm`